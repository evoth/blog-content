---
title: Perpetual Timelapse
summary: "An automatic time-lapse creation and posting system (my first Python project)"
weight: 50
resources:
  - name: thumb
    src: ptl-thumb.svg
    params:
      alt: Circle split between sun and moon/stars, encircled by cyclic arrows.
      loopSeconds: 3.0
thumbAsHero: true
links:
    - title: YouTube Channel
      url: https://www.youtube.com/@perpetualtimelapse9938
languages:
    - Python
tags:
    - YouTube API
    - GoPro WiFi API
---

Perpetual Timelapse{{< sidenote "(" ")" >}}named before I knew that "time-lapse" with a hyphen is more correct{{< /sidenote >}} wasn't my first big programming project, but it was the first that wasn't bound by the [Scratch](https://scratch.mit.edu/) canvas or the screen of my [calculator](https://www.cemetech.net/downloads/users/Pi_Runner). I started development just before the beginning of 2020, and the resulting system uploaded daily time-lapses to [YouTube](https://www.youtube.com/@perpetualtimelapse9938) on most days from April 9th to June 1st, 2020{{< sidenote "(" ")" >}}the system was also operational and uploading videos privately during development in the preceding months{{< /sidenote >}}. During this time, the system processed and uploaded over 16 hours of video, representing over 660 hours of time-lapse recording. Although the final iteration of the system took longer than expected to develop and presented reliability issues, I gained valuable programming/integration experience and increased confidence in my abilities to tackle complex problems.

## Inspiration

In late 2019, I was interested in filming time-lapses, mainly of the clouds and weather throughout the day. I also wanted get my hands dirty with a "real" programming language, so I set a goal to create a system that could film daily time-lapse videos and upload them to YouTube, all with no (or very minimal) human input.

By searching on YouTube, I had seen a few channels that were similar to my vision: daily time-lapses from sunrise to sunset. Some of them had fancy auto-generated thumbnails and descriptions, and sometimes even music, so these became additional features that I wanted to implement eventually. Examples of these channels that I saw (and sometimes even communicated with the creators of) were [Daily Timelapses](https://www.youtube.com/@DailyTimelapses/videos), [Time Lapse](https://www.youtube.com/@timelapse4145/videos), and [Tigh Ban Lek](https://www.youtube.com/@TighBanLek/videos).{{< sidenote >}}Other examples include [Synekism Inspire](https://www.youtube.com/@SynekismInspire/videos), [GistTime](https://www.youtube.com/@GistTime/videos), [charlieums](https://www.youtube.com/@timelapse713/videos), and [Ridgeline Sky](https://www.youtube.com/@RidgelineSky/videos).{{< /sidenote >}} It's clear that these channels aren't motivated by views (they often have 10 times more videos than subscribers), but I find it strangely soothing to watch a day passing in a place that I've never been and just watch the clouds drift over the landscape.

Anyways, that's how, on December 25th, 2019, I set out to build this system. Not only that, but I wanted to start uploading on the new year, only a week later. That may seem overly ambitious (and it was), but I actually did manage to get some sort of system set up by then. It was the iteration process on that initial system that extended the project into a months-long endeavor that persisted into the 2020 quarantine.

## Process

I chose to use Python for the project, mainly because of its reputation for being powerful and easy to learn. Since I hadn't written in Python before, there was a learning curve, but as the project progressed it became easier to work with as I learned the basic features of the language.

### Initial Version (Phone)

My first plan involved controlling a phone programmatically to take individual time-lapse frames and transfer them to the computer during daylight hours. Then, they would be combined into the final video and uploaded, ideally during the night.

So, I started by making a program to repeatedly call [Android Debug Bridge](/concepts/adb) to trigger the shutter on the phone and transfer each frame to the computer. Then, when the day's frames had been captured, [FFmpeg](https://ffmpeg.org/) was used to create a video from the frames, and the video was uploaded with the YouTube API (though I used a script called [youtube-upload](https://github.com/tokland/youtube-upload) since I had no experience with APIs at the time).

This version of the system was ready by New Year's 2020, but I had only been able to test it over short durations up to that point. When it came time to film the time-lapse for January 1st, the problems with the initial setup became apparent:
1. The phone would overheat from being in the sunny window
2. The phone would randomly disconnect from the computer
3. The phone would periodically lose focus, even though it was set to infinite

As it turns out, a phone is not built for taking thousands of photos while continuously connected to a computer and baking in the sun. After this realization, I spent a couple months testing and honing the other parts of the system while using an old webcam to take the actual frames.{{< sidenote >}}The webcam had a maximum focal distance of about 5 feet, making it unusable as the actual camera.{{< /sidenote >}} At this point, I probably could have just bought a nicer webcam and called it a day, but I was hesitant to spend money on the project.

### Improved Version (GoPro)

Luckily, I remembered that I had an old GoPro that could be used instead. I had previously disregarded that idea since I didn't think it would be possible to control the GoPro or transfer the footage to a computer without human intervention. When I further researched the topic, though, I found that the [GoPro WiFi commands](https://github.com/KonradIT/goprowifihack) had been documented by the legendary [KonradIT](https://github.com/KonradIT), meaning that it might indeed be possible to use the GoPro. Another advantage to this approach is that I could use its built-in time-lapse feature, eliminating the need to combine the frames on the computer.

However, there were still major challenges to overcome, namely staying connected to the GoPro's WiFi network and transferring multiple gigabytes of video over it every day. Thanks to the [goprocam](https://github.com/KonradIT/gopro-py-api) Python module, I could easily send commands to the GoPro, but it took a lot of trial and error before I could reliably keep the WiFi network alive so that the time-lapse could be started at dawn and ended at dusk.

Then, I had to figure out how to download the video, which typically came in the form of multiple video segments topping out at 4GB each. In the end, this involved querying video metadata through the WiFi commands before downloading each segment with a fine-tuned [Wget](https://en.wikipedia.org/wiki/Wget) command. These steps worked most of the time, but because the GoPro couldn't record and transfer files at the same time, the video had to be completely downloaded overnight, or else the system would fall behind. As you might imagine, this tended to happen frequently due to the fragile nature of the whole setup.

Reliability issues notwithstanding, the new setup using the GoPro is the one that ran from April to June 2020. But what happened to the videos after they had been transferred?

### Video Creation and Packaging

With the day's time-lapse video downloaded to the computer, the program made three different versions at different speeds (short, medium, and long), again using FFmpeg.{{< sidenote >}}[Long](https://www.youtube.com/playlist?list=PLjp_XA8ELhxlpSjM_ziNge-GTFAGuLDj5), [medium](https://www.youtube.com/playlist?list=PLjp_XA8ELhxkLQww99kvMXVYITjTk7Ruz), and [short](https://www.youtube.com/playlist?list=PLjp_XA8ELhxmvBMpizHbnpjqMsf17a1Z4) represented 60x, 180x, and 540x faster than realtime, respectively.{{< /sidenote >}} Then, a thumbnail was generated programmatically using [ImageMagick](https://www.imagemagick.org/), and songs were selected from a hand-picked royalty-free music library to fit the length of the video. As time progressed, I also started added more fun metadata to the video description, and towards the end even made a system to detect "good" sunsets/sunrises and upload separate videos for those.

With the videos processed and ready to go, they would then be uploaded to YouTube, likely during the morning hours as the next day's time-lapse had already started. At least, if everything had gone according to plan.

## Lessons

The lessons that I learned from this endeavor boil down to two main ideas:
1. Ability to change directions from initial plans
2. Self-reliance and confidence in problem solving (given enough time)

First, I was stuck for a while as I tried to make my original idea work. But when I took the time to assess all of my available resources, that opened up more possible ways to solve the problem. Then, I could evaluate the tradeoffs between these different approaches to find the most practical solution. Today, I like this "backtracking" aspect of problem solving because it often leads to surprising methods to overcome or circumnavigate roadblocks in the development process.{{< sidenote "(" ")" >}}Although I'd like to think these "surprising" solutions are usually elegant, sometimes they can be "surprisingly" hacky...{{< /sidenote >}}

Which leads to the second point: that working on this project fueled my self-reliance and confidence that I could solve any problem (within reason), at least given enough time. On one hand, this has been a motivating factor in all of my personal projects since. If I have a vision that seems out of reach at first, but I can break it into manageable pieces and solve each of those, then I can compose them into something awesome. However, that last part, _time_, is something that I'm still improving on today. I've gotten much better at giving myself reasonable deadlines and limiting scope if necessary, but sometimes it can still be a challenge, especially when working in unfamiliar territory.

As a whole, I'm still proud of this project, and of myself for making the jump into "real" programming that led to where I am today.