---
name: watch-video
description: >-
  Let an agent actually "watch" a video or reel — download it, extract timestamped frames and a
  timestamped transcript, then read the frames as images. Use when the user shares a video URL or
  local file and asks what is in it, what someone said, to summarize it, find a moment, pull
  quotes, critique visuals, or extract on-screen text. Works with YouTube, TikTok, Instagram
  reels, X, Loom and local mp4/mov/mkv/webm files.
---

# Watch video

An agent cannot ingest video directly — only images and text. This skill converts a video into
both: **timestamped frames** (read as images) plus a **timestamped transcript**. Reading them
together is what "watching" means here.

## When to activate

- A video URL is shared and the user asks anything about its contents.
- "What happens in this reel?" / "Summarize this video" / "What did they say at 2:30?"
- "Pull the on-screen text" / "What is the hook in the first three seconds?"
- A local video file is referenced and the user asks about its content.

Do **not** activate for downloading only — that is a downloader's job.

## Modes and cost

Image tokens scale roughly with `width × height / 750`. At a 768 px default each frame is about
440 tokens. Cost comes from frames, not the transcript.

| Question | Mode | Approximate tokens |
|----------|------|--------------------|
| "What did they say?" | `transcript` | ~0 image tokens |
| "Summarize this 30s reel" | `balanced` | ~10–25k |
| "Find the moment X happens" | `transcript` first, then a focused window | ~5k |
| "Read the text on screen" | OCR mode, few frames | ~15k |
| "Critique the edit / pacing" | `balanced`, more frames | ~26k |

Default to transcript-only for anything longer than about five minutes: locate the moment in text,
then spend frames only on the window that matters. If a run reports more than ~40k tokens, reduce
the frame cap or focus a window before reading everything.

## Workflow

1. Run the extractor script with the chosen mode. Note the reported frame count and token estimate.
2. Read the manifest it emits — the transcript is carried inline.
3. Read every listed frame **in order**. Frame filenames carry their source timestamp, so visual
   observations can be cited by time.
4. Answer from frames and transcript together. Cite timestamps.

## Useful options

| Option | Purpose |
|--------|---------|
| transcript-only | Captions/transcript, zero frames — fastest, often no download |
| uniform vs scene-change sampling | Uniform caps a fixed count; scene-change keeps one frame per distinct shot |
| `--start` / `--end` | Focused window; downloads only that section |
| frame cap / width override | Control token budget and resolution |
| OCR preprocessing | Grayscale + contrast + sharpen for on-screen text |
| browser cookies | Login-walled social content |
| language / model / vocabulary prompt | Transcript accuracy; a vocabulary prompt matters more than model size |
| keep work directory | Reuse prior extraction instead of rebuilding |

## Transcript sources

1. **Native captions** via the downloader — free, instant, often no video download.
2. **Local Whisper fallback** — runs offline, no API key; a small English model plus a technical
   vocabulary prompt usually beats a larger model with no prompt. Reserve larger models for hard
   audio (heavy accents, noise, crosstalk).

A silent clip yields no transcript and the manifest says "visual only" — that is not an error.

## Troubleshooting

- HTTP 403 / signature errors → the downloader is stale; upgrade it.
- Empty transcript → no speech, captions unavailable, or no local Whisper model.
- Rate limits on captions → request specific languages, not broad wildcards.
- Portrait reels cap the **longest** side, so a 9:16 frame is much cheaper than a landscape one.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `watch-video` from
ryankolean/summit-claude-skills. The referenced script is an external tool and is not bundled here.

- Source: https://github.com/ryankolean/summit-claude-skills/tree/main/skills/watch-video
- License: MIT — Copyright (c) 2026 Summit Software Solutions LLC.
- No upstream source files are copied verbatim.
