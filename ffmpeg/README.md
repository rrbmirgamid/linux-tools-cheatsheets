# ffmpeg Cheat Sheet

A short reference for common `ffmpeg` media operations.

## Merge video and audio

MP4:

```bash
ffmpeg -i video.mp4 -i audio.m4a -c:v copy -c:a copy output.mp4
```

MKV:

```bash
ffmpeg -i video.mp4 -i audio.webm -c:v copy -c:a copy output.mkv
```

## Extract audio

Convert audio from MP4 to MP3:

```bash
ffmpeg -i video.mp4 -vn -acodec libmp3lame -ac 2 -ab 160k -ar 48000 audio.mp3
```

Convert audio from WebM to MP3:

```bash
ffmpeg -i file.webm -vn -ab 128k -ar 44100 -y file.mp3
```

## Cut / trim media

Extract 214 seconds starting at `00:00:11.550`:

```bash
ffmpeg -t 214 -ss 00:00:11.550 -i inputfile.mp3 -acodec copy outputfile.mp3
```

Extract from `00:00:20` to `00:00:40`:

```bash
ffmpeg -i test.mp3 -ss 00:00:20 -to 00:00:40 -c copy -y temp.mp3
```

Extract 25 seconds starting at `00:04:22`:

```bash
ffmpeg -i input.mkv -ss 00:04:22 -t 00:00:25 -c copy cut.mkv
```

## Scale video resolution

Reduce width and height by half:

```bash
ffmpeg -i input.mkv -vf "scale=iw/2:ih/2" half_the_frame_size.mkv
```

Reduce width and height to one third:

```bash
ffmpeg -i input.mkv -vf "scale=iw/3:ih/3" third_the_frame_size.mkv
```

## Quick reference

```bash
ffmpeg -i video.mp4 -i audio.m4a -c:v copy -c:a copy output.mp4
ffmpeg -i video.mp4 -vn -acodec libmp3lame audio.mp3
ffmpeg -i input.mp3 -ss 00:00:20 -to 00:00:40 -c copy output.mp3
ffmpeg -i input.mkv -vf "scale=iw/2:ih/2" output.mkv
```
