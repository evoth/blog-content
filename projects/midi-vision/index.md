---
title: Midi Vision
summary: "Visualizing midi files as a chorus of colorful lines using Tone.js and the canvas"
weight: 60
resources:
  - name: thumb
    src: midi-vision-thumb.svg
    params:
      alt: Glowing aquamarine-colored zigzag shape on a black background.
thumbAsHero: true
links:
    - title: GitHub Repository
      url: https://github.com/evoth/midi-vision
    - title: Web App
      url: https://midi.ethanvoth.com
---

Check back soon for more detailed insight on this project's inspiration, process, and lessons! For now, here's information from the [GitHub repo](https://github.com/evoth/midi-vision):

## Inspiration
The singular inspiration for this project is a video titled [Bach Vision Test](https://www.youtube.com/watch?v=vJfiOuDdetg), released by the band [Vulfpeck](https://vulfpeck.com), with visuals by [Rob Stenson](https://robstenson.com).

## Instructions
- **Warning:** This project is very bare-bones at the moment, so you might run into glitches.
- **Upload file:** Press the "Choose file" button (try to use a file with 4 tracks or less).
- **Play file:** Press the "Play file" button to start playing/visualizing the file.
- **Pause/stop:** As of now there are no controls for pausing/stopping, so just refresh the page to reset.

## Known bugs
- New rendering method does not support Firefox because it does not support importing module scripts in a web worker. See [this Stack Overflow answer](https://stackoverflow.com/a/45578811) and [this Mozilla bug thread](https://bugzilla.mozilla.org/show_bug.cgi?id=1247687).

## Todo
- Fix artifact on the boundary of realtime and pre-rendered due to differing contributions from blur outside of the render boundaries
- Type hinting?
- Figure out weird delay
- CRACKLE
- replace forEach with let of for consistency
- Fix repeated notes
- "How it works" section of README