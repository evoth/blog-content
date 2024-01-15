---
date: 2023-07-26T10:04:44-06:00
title: Automatic Time-Lapses with ADB and FFmpeg
summary: Programmatically creating time-lapses with Python and an old Android phone
slug: ptl-adb-ffmpeg
resources:
- name: thumb
  src:
  params:
    alt:
projects:
- ptl
series:
- projects
concepts:
- adb
tags:
draft: true
publishDate:
---

{{< todo >}}tenses{{< /todo >}}By December 25th, 2019, I had never written a program in a "real" programming language, besides some tiny JavaScript webpages a few years prior. But, since my next project couldn't be done in [Scratch](https://scratch.mit.edu) or on my calculator (my previous development platforms of choice), that would need to change. At the time, I loved filming and watching time-lapses{{< todo >}}Link or explanation{{< /todo >}}, so my idea was to create a system that automatically films daily time-lapse videos and uploads them to YouTube. Furthermore, my goal was to have the system up and running by January 1st, 2020, in less than a week.

I chose to use Python for the project, partly because of its reputation as an easy-to-learn language, and partly because I had utilized some Python scripts before, so I was confident that it could be used to accomplish what I needed. Throughout the project, I would search things like "Python if statements", "Python run terminal commands", and "How to access API with Python". This way, I could start working immediately and learn as I go, without first needing to spend time acquiring background knowledge.{{< sidenote >}}When learning something like this, the trade off is that I inevitably pick up some bad practices or do things in a suboptimal way. Personally, though, I find it easier to motivate myself by working hands-on rather than learning all of the theory beforehand. In recent years, I've gotten better at seeking out the "correct" way of accomplishing something before adopting it as a habit, and I've also started to enjoy reading up about a prospective tool before I dive into the deep end.{{< /sidenote >}} Although this isn't always the best way to learn a new tool, my self-imposed 1 week deadline meant I had little time to do otherwise.

After choosing which language to use, the next step was to break up the overall problem (an automatic time-lapse filming and uploading system) into manageable pieces. The first task, and the topic of this post, was to programmatically film and render a time-lapse.

## Recording Time-Lapse Frames

A time-lapse is simply a video that's played back at a faster frame rate than the frame rate used to film it. So, my initial idea for creating a time-lapse was to control a device that would capture individual frames at regular intervals, while somehow transferring these frames to the controlling computer. Then, the sequence of frames (with an interval of a few seconds between each frame) could be rendered into a single video at a normal framerate like 30fps. The result is a video that spans multiple hours, or even a day, condensed into a few minutes.

Since I had an old Android phone that could be dedicated to the project, I chose to use its camera to capture the frames. In order to do so, I needed a way to programmatically trigger the phone's shutter and transfer the photos to the computer. This brings us to ADB.

{{< concept "adb" 2 >}}

### Triggering the shutter

With the Android phone turned on and open to a camera app, the shutter could be triggered using one of the volume buttons. So, I first tried simulating this action with ADB by running the following on the computer connected to the phone:
{{< todo >}}Check all this for accuracy and formatting as I'm on a plane right now working with limited resources{{< /todo >}}

```
adb shell input keyevent KEYCODE_VOLUME_UP
```

The `adb shell` part means that the command is run on the Android device (client), allowing us to control it over USB. The rest of the command, `input keyevent KEYCODE_VOLUME_UP`, does exactly what it sounds like, triggering a "volume up" key event. However, the command was too specific, since it only adjusted the volume instead of triggering the camera shutter. It turns out that there's a separate key code for this exact purpose:

```
adb shell input keyevent KEYCODE_CAMERA
```

Now, I could take frames with the camera, but needed to figure out how to transfer them onto the computer.

### Transferring frames

To copy the frames from the camera app (Free Camera) directory on the phone to a directory named `temp` on the commuter, I used the `adb pull` command:

```
adb pull /storage/emulated/legacy/DCIM/FreeCamera/ temp
```

And to delete a frame from the phone once it had been copied, I once again used the `adb shell` command, this time with the common `rm` utility:

```
adb shell rm /storage/emulated/legacy/DCIM/FreeCamera/<FILENAME>
```

### Code

Now, I was ready to make a simple Python proof of concept. As this was my very first time programming in Python, I would say my original implementation was *questionable*. Regardless, I'll walk through my original code, then discuss some of the issues with it, including what I would do differently today.

Here's the first version of the test script that implements the commands from above:

```python
from subprocess import call
import time
from datetime import datetime
import shutil
import os

storage_path = '/home/ptl/PTL/'

call(['adb','shell','rm','/storage/emulated/legacy/DCIM/FreeCamera/*'])
for i in range(20):
	time_debug = time.time()	
	call(['adb','shell','input','keyevent + CAMERA'])
	photo_time = int(time.time())	
	#time.sleep(0.7)
	call(['adb','pull','/storage/emulated/legacy/DCIM/FreeCamera/',storage_path+'temp'])
	for filename in os.listdir(storage_path+'temp/FreeCamera/'):		
		call(['adb','shell','rm','/storage/emulated/legacy/DCIM/FreeCamera/'+filename])		
		shutil.move(storage_path+'temp/FreeCamera/'+filename, storage_path+'Frames/'+str(photo_time)+'.jpg')
	print(time.time()-time_debug)
```

### Issues

## Combining Frames


