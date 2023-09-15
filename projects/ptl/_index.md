---
title: Perpetual Timelapse
summary: "An automatic time-lapse creation and posting system (my first Python project)"
resources:
  - name: thumb
    src: ptl-thumb.svg
    params:
      alt: Looping animation of arrows spinning in a circle, enclosing two semicircles which represent night and day.
      loopSeconds: 3.0
  - name: hero
    src: ptl-hero.svg
    params:
      alt: Looping animation of arrows spinning in a circle, enclosing two semicircles which represent night and day.
      loopSeconds: 3.0
---

Perpetual Timelapse{{< sidenote "(" ")" "" "" >}}I named it before I knew that "time-lapse" with a hyphen is more correct{{< /sidenote >}} wasn't my first big programming project, but it was the first that wasn't bound by the Scratch canvas or the screen of my calculator. I started development just before the beginning of 2020, and the resulting system uploaded daily time-lapses to YouTube on most days from April 9th to June 1st, 2020{{< sidenote "(" ")" "" "" >}}although the system was also operational and uploading videos privately in the preceding months during development{{< /sidenote >}}. During this time, the system processed and uploaded over 16 hours of video, representing over 660 hours of time-lapse recording. Although the final iteration of the system took longer than expected to develop and presented reliability issues, I gained valuable programming/integration experience and gained confidence in my abilities to tackle complex problems.

## Inspiration

In late 2019, I was interested in filming time-lapses, mainly of the clouds and weather throughout the day. I also wanted get my hands dirty with a "real" programming language, so I set a goal to create a system that could film daily time-lapse videos and upload them to YouTube, all with no (or very minimal) human input.

By searching on YouTube, I had seen a few channels that were similar to my vision: daily time-lapses from sunrise to sunset. Some of them had fancy auto-generated thumbnails and descriptions, and sometimes even music, so these became additional features that I wanted to implement eventually. Examples of these channels that I saw (and sometimes even communicated with the creators of) were [Daily Timelapses](https://www.youtube.com/@DailyTimelapses/videos), [Time Lapse](https://www.youtube.com/@timelapse4145/videos), and [Tigh Ban Lek](https://www.youtube.com/@TighBanLek/videos).{{< sidenote >}}Other examples include [Synekism Inspire](https://www.youtube.com/@SynekismInspire/videos), [GistTime](https://www.youtube.com/@GistTime/videos), [charlieums](https://www.youtube.com/@timelapse713/videos), and [Ridgeline Sky](https://www.youtube.com/@RidgelineSky/videos).{{< /sidenote >}} It's clear that these channels aren't motivated by views (they often have 10 times more videos than subscribers), but I find it surprisingly soothing to watch a day passing in a place that I've never been and just watch the clouds drift over the landscape.

Anyways, that's how, on December 25th, 2019, I set out to build this system. Not only that, but I wanted to start uploading on the new year, only a week later! That may seem overly ambitious (and it was), but I actually did manage to get some sort of system set up by then. It was the iteration process on that initial system that extended the project into a months-long endeavor that persisted into the 2020 quarantine.
