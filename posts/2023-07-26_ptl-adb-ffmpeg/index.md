---
date: 2023-07-26T10:04:44-06:00
title: Automatic Time-Lapses with ADB and FFmpeg
summary: Programmatically creating time-lapses with an old Android phone and Python
slug: ptl-adb-ffmpeg
resources:
projects:
  - ptl
series:
concepts:
  - adb
tags:
draft: true
publishDate:
---

By December 25th, 2019, I had never written a program in a "real" programming language, besides some tiny JavaScript webpages a few years prior. But, since my next project couldn't be done in [Scratch](https://scratch.mit.edu) or on my calculator (my previous development platforms of choice), that would need to change. At the time, I loved filming and watching time-lapses{{< todo >}}Link or explanation{{< /todo >}}, so my idea was to create a system that automatically films daily time-lapse videos and uploads them to YouTube. Furthermore, my goal was to have the system up and running by January 1st, 2020, in less than a week.

I chose to use Python for the project, partly because of its reputation as an easy-to-learn language, and partly because I had utilized some Python scripts before, so I was confident that it could be used to accomplish what I needed. Throughout the project, I would search things like "Python if statements", "Python run terminal commands", and "How to access API with Python". This way, I could start working immediately and learn as I go, without first needing to spend time acquiring background knowledge.{{< sidenote >}}When learning something like this, the trade off is that I inevitably pick up some bad practices or do things in a suboptimal way. Personally, though, I find it easier to motivate myself by working hands-on rather than learning all of the theory beforehand. In recent years, I've gotten better at seeking out the "correct" way of accomplishing something before adopting it as a habit, but I've also started to enjoy reading up about a prospective tool before I dive into the deep end.{{< /sidenote >}} Although this isn't always the best way to learn a new tool, my self-imposed 1 week deadline meant I had little time to do otherwise.

After choosing which language to use, the next step was to break up the overall problem (an automatic time-lapse filming and uploading system) into manageable pieces. The first task, and the topic of this post, was to programmatically film and render a time-lapse.

## Recording Time-Lapse Frames

A time-lapse is simply a video that's played back at a faster frame rate than the frame rate used to film it. So, my initial idea for creating a time-lapse was to control a device that would capture individual frames at regular intervals, while somehow transferring these frames to the controlling computer. Then, the sequence of frames (with an interval of a few seconds between each frame) could be rendered into a single video at a normal framerate like 30fps. The result is a video that spans multiple hours, or even a day, condensed into a few minutes.

Since I had an old Android phone that could be dedicated to the project, I chose to use its camera to capture the frames. In order to do so, I needed a way to programmatically trigger the phone's shutter and transfer the photos to the computer. This brings us to ADB.

{{< concept "adb" >}}

### Triggering the shutter

### Transferring frames

### Code

### Issues

## Combining Frames


