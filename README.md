# Handling audio and video with ffmpeg

## Introduction

>[FFmpeg](https://ffmpeg.org/) is a **free and open-source** software project consisting of a suite of libraries and programs for handling video, audio, and other multimedia files and streams. At its core is the command-line `ffmpeg` tool itself, designed for processing of video and audio files.

## Basic Usages

- Format convertion and transcoding
- Trimming
- Concatenation

## Basic Structure and Syntax

>ffmpeg [global_options] {[input_file_options] -i input_url} ... {[output_file_options] output_url} ...

## Basic Examples

- Convert MP4 video to AVI.

```bash
ffmpeg -i input.mp4 output.avi
```

- Extract the sound from a video and save it as AAC.

```bash
ffmpeg -i input-video.mp4 -vn output-audio.aac
```

- Convert TS video to MP4. AAC Audio, h264 Video.

```bash
ffmpeg -i input.ts -c:a aac -c:v h264 output.mp4
```

- Trim a video from a given start time and duration (omit the -t flag to trim till the end)

```bash
ffmpeg -i input.mov -ss 0ms -t 10000ms output.mov
```

- Concatenate two AAC files without re-encoding

```bash
ffmpeg -i "concat:input1.aac|input2.aac" -acodec copy output.aac
```

## [ffmpy3](https://github.com/wchill/ffmpy3)

>A simple asynchronous Python wrapper for ffmpeg

```python
from ffmpy3 import FFmpeg
ff = FFmpeg(
    inputs={"input.mp4": ["-ss","5000ms","-t","10000ms"]},
    outputs={"output.mov": "-c:a copy -c:v copy"}
)
print(ff.cmd)
# ffmpeg -ss 5000ms -t 10000ms -i input.mp4 -c:a copy -c:v copy output.mov
ff.run()
```
