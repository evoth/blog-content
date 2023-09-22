---
title: GoPro Video Sync
summary: "Tool to sync videos from two jointly mounted GoPros using data from multiple sensors"
weight: 20
resources:
  - name: thumb
    src: gopro-video-sync-thumb.svg
    params:
      alt: Dramatic vector art of a GoPro combined with a clapboard.
thumbAsHero: true
links:
    - title: GitHub Repository
      url: https://github.com/evoth/gopro-video-sync
    - title: PyPI Package
      url: https://pypi.org/project/gopro-video-sync/
---

Check back soon for more detailed insight on this project's inspiration, process, and lessons! For now, here's information from the [GitHub repo](https://github.com/evoth/gopro-video-sync):

## Installation

Install `gopro-video-sync` from PyPI:

```bash
pip install gopro-video-sync
```

Or from the source on GitHub:

```bash
pip install "gopro-video-sync @ git+https://github.com/evoth/gopro-video-sync"
```

The package will be installed with the module name `gopro_video_sync`.

## Usage example

Print the required adjustment to sync videos from two jointly mounted GoPros:

```python
from gopro_video_sync import gopro_offset

video_1 = "GOPR1569.MP4"
video_2 = "GOPR0105.MP4"

offset, source_1, source_2 = gopro_offset(video_1, video_2)

if offset is None:
    print("Could not determine offset between the given videos.")
else:
    offset = round(offset, 3)
    if offset > 0:
        print(f"Trim the first {offset} seconds of {video_1} to sync the videos.")
    elif offset < 0:
        print(f"Trim the first {-1 * offset} seconds of {video_2} to sync the videos.")
    else:
        print("Videos are already synced.")
```

## How it works

Since I had wanted to sync videos from two GoPros that were mounted together, I realized that the gyroscope and accelerometer information from each should be identical. GoPros store sensor data inside MP4 files in a format called [GPMF](https://github.com/gopro/gpmf-parser), developed by GoPro for this very purpose. So, this program extracts the GPMF data from each video file and uses [cross-correlation](https://en.wikipedia.org/wiki/Cross-correlation) to attempt to line up the videos.

If the individual offsets obtained from the gyroscope and accelerometer data do not agree, then the audio data is used in an attempt to verify one of the sensor offsets. If this does not work, then the offset can not be determined.
