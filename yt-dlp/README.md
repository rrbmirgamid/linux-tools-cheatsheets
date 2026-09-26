# yt-dlp Cheat Sheet

`yt-dlp` is a command-line audio/video downloader and a modern successor to `youtube-dl`.

## Install

On Ubuntu/Debian:

```bash
sudo apt update
sudo apt install yt-dlp
```

If installed as the official release binary, update with:

```bash
yt-dlp -U
```

For `pip` installations, update using the same `pip install -U ...` command you used to install it.

> `ffmpeg` and `ffprobe` are strongly recommended. They are required for merging separate video/audio streams and for many post-processing tasks.

## Basic usage

Download using the default best-quality selection:

```bash
yt-dlp <url>
```

List available formats:

```bash
yt-dlp -F <url>
```

Download a specific format:

```bash
yt-dlp -f <format_id> <url>
```

## Best video + audio

Explicitly request the best video and best audio, with a fallback to the best combined format:

```bash
yt-dlp -f "bestvideo*+bestaudio/best" <url>
```

In most cases, plain `yt-dlp <url>` already selects the best available quality automatically.

## Audio only

Download the best available audio:

```bash
yt-dlp -f bestaudio <url>
```

Extract audio as MP3:

```bash
yt-dlp -x --audio-format mp3 --audio-quality 0 <url>
```

## Merge output as MP4

```bash
yt-dlp -f "bestvideo*+bestaudio/best" --merge-output-format mp4 <url>
```

## Playlists

Download a playlist:

```bash
yt-dlp <playlist_url>
```

Continue past unavailable or failed entries:

```bash
yt-dlp --ignore-errors <playlist_url>
```

## Useful examples

Show filenames without downloading:

```bash
yt-dlp --get-filename <url>
```

Download to a custom filename template:

```bash
yt-dlp -o "%(title)s.%(ext)s" <url>
```

Download subtitles:

```bash
yt-dlp --write-subs <url>
```

Download automatically generated subtitles:

```bash
yt-dlp --write-auto-subs <url>
```

## Quick reference

```bash
yt-dlp <url>                                      # Download best available quality
yt-dlp -F <url>                                   # List formats
yt-dlp -f <format_id> <url>                       # Download a specific format
yt-dlp -f "bestvideo*+bestaudio/best" <url>       # Best video + audio
yt-dlp -f bestaudio <url>                         # Best audio stream
yt-dlp -x --audio-format mp3 --audio-quality 0 <url>  # Extract MP3
yt-dlp --merge-output-format mp4 <url>            # Prefer MP4 when merging
yt-dlp --ignore-errors <playlist_url>              # Continue playlist on errors
```
