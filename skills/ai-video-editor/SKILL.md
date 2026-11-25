---
name: ai-video-editor
description: >-
  Turn natural-language requests into ffmpeg and yt-dlp commands: trim, cut, merge, remove silence,
  normalize audio, burn subtitles, extract audio, create shorts/reels, download and clip YouTube
  videos, batch-process folders and apply social-media presets. Use when the user asks to edit a
  local video or audio file or clip a YouTube video without leaving the terminal.
---

# AI video editor

A lightweight, command-first editor built on `ffmpeg` and `yt-dlp`. Describe the result in plain
language; this skill produces and runs the right commands.

## Prerequisites

```bash
# macOS
brew install ffmpeg && pip install yt-dlp
# Linux
sudo apt install ffmpeg && pip install yt-dlp
# Windows
winget install FFmpeg && winget install yt-dlp
```

## Capabilities

- **Trim / cut** losslessly (no re-encode where possible).
- **Remove silence** — auto-edit podcasts.
- **Normalize** audio levels (loudness target).
- **Subtitles** — burn in or embed SRT.
- **Extract audio** to MP3 / WAV / AAC.
- **YouTube** — download and clip by timestamp via yt-dlp.
- **Shorts / reels** — 9:16 crop or pad from long videos.
- **Merge** clips; **batch-process** a folder.
- **Presets** — Reel/TikTok, Instagram post, YouTube Shorts, LinkedIn.
- Fades, speed changes, background-music mixing, frame / GIF extraction.

## Workflow

1. **Resolve the input** — local path or URL. For a URL, confirm yt-dlp can access it before
   planning the edit.
2. **Clarify only what matters** — output path, in/out points, target aspect ratio. If a preset is
   named, use its documented dimensions and duration.
3. **Prefer lossless operations** where the cut points allow it; re-encode only when the edit
   requires it (e.g. a crop, speed change or overlay).
4. **Run the command**, then verify the output exists and has the expected duration with `ffprobe`.
5. **Report** the output path and the key operation. Never overwrite the source file — write a new
   output and ask before replacing the original.

## Command patterns

Adapt flags to the installed ffmpeg version.

```bash
# lossless trim by stream copy (keyframe-aligned)
ffmpeg -ss 00:00:30 -to 00:01:45 -i input.mp4 -c copy -avoid_negative_ts make_zero out.mp4

# re-encode trim (frame-accurate)
ffmpeg -ss 00:00:30 -to 00:01:45 -i input.mp4 -c:v libx264 -c:a aac out.mp4

# 9:16 short with pad
ffmpeg -i input.mp4 -vf "scale=1080:1920:force_original_aspect_ratio=decrease,pad=1080:1920:(ow-iw)/2:(oh-ih)/2" -c:a copy short.mp4

# burn subtitles
ffmpeg -i input.mp4 -vf "subtitles=subs.srt" -c:a copy captioned.mp4

# remove silence
ffmpeg -i input.wav -af "silenceremove=start_periods=1:start_duration=0.3:start_threshold=-40dB" cleaned.wav

# download a YouTube segment
yt-dlp --download-sections "*00:00:30-00:01:45" -f "bv*+ba/b" "<url>" -o clip.%(ext)s
```

## Rules

- Never invent subtitle text — only burn text the user supplied or that a transcription step
  produced.
- For subtitles, use absolute paths with no special characters on Windows.
- For multi-step edits, write a short shell script the user can rerun rather than a long one-off
  command.
- Pair with a transcription / timestamp skill when the cut points come from speech.
- This skill edits existing media only; it does not generate new footage.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `ai-video-editor` from
shahafg1/ai-video-editor.

- Source: https://github.com/shahafg1/ai-video-editor
- License: MIT, shahafg1.
- No upstream source files are copied verbatim.
