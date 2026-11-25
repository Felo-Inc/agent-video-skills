---
name: video-to-shorts
description: >-
  Turn one long video — a podcast, interview, talk, webinar, stream or YouTube video — into
  finished vertical shorts for TikTok, Reels and Shorts. Transcribes with word timestamps, scores
  candidate moments for hook/standalone/payoff, cuts and captions each one. Use when the user says
  "long to short", "clip my podcast", "repurpose this video", "make shorts from this video".
---

# Long video to shorts

A Short cut from a long video is not "the best moment". It is a moment that **survives without the
video around it** — a much smaller set. The job is to find those moments, rewrite their opening for
a cold viewer, and deliver a finished vertical clip.

## Preflight

Check the required tools are available (a downloader, ffmpeg, a transcription path) before
starting. Anything missing: guide the user to install it rather than proceeding with a partial
pipeline. Confirm the source is something the user owns or has permission to reuse.

## 1. Get a transcript with timestamps

- Prefer existing captions/chapters from the platform (free, fast).
- Otherwise transcribe the local file with a local speech engine (offline, no key) or the user's own
  API key.
- Word-level timing matters — it drives caption highlighting and precise cut points.

## 2. Find candidate moments

Scan the transcript for spans of roughly 20–60 seconds where **all three** hold:

1. **Opens on a complete thought** — if the first sentence needs the previous minute, it is not a Short.
2. **Contains a turn** — a claim, then something that complicates or proves it.
3. **Ends on a line**, not a trail-off.

Score candidates on hook strength, standalone clarity and payoff. Show the user the top five with
timecodes and first lines so they can reject one without reading the whole transcript. If an idea
is too spread out to clip, write a fresh script from it instead of forcing a cut.

## 3. Write each Short

- **A new first line.** The long video's opener assumes context this viewer lacks — write a
  replacement hook.
- **On-screen text for the first two seconds**, with different words from the spoken line.
- **A loop point** — what the last line sets up that the first line answers.
- **Vertical framing note** — what gets cropped from a 16:9 frame and whether it matters.
- **Captions** — word-by-word, burned in, inside the platform safe zone.
- **Audio** — remove pauses, normalize loudness, duck music under speech.
- **Title and caption text** for the post.

## 4. Cut and deliver

Cut at 1080×1920 with ffmpeg, keep the speaker in frame, burn the captions, write metadata beside
each clip. Deliver a short list of finished files with their source timecodes.

## Rules

- Nothing here publishes. Each run ends with the user's decision: **ship it or change it?**
- Clip only material the user owns or is licensed to reuse.
- Never invent a quote — the spoken words come from the transcript or a clearly labelled new script.
- No silent auto-posting; if a publishing integration exists, it needs a separate explicit OK.
- A high hook rate with poor retention is not a win — check that the clip pays off, not just that it
  opens well.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `video-to-shorts-skill` from
social-media-skills, `yt-shorts` from Jakeschincariol/youtube-agent-skill, and `clips` from
Melvynx/video-agent-skills — all MIT. Referenced scripts and engines are external and not bundled.

- Sources:
  - https://github.com/social-media-skills/video-to-shorts-skill
  - https://github.com/Jakeschincariol/youtube-agent-skill/tree/main/skills/yt-shorts
  - https://github.com/Melvynx/video-agent-skills/tree/main/skills/clips
- License: MIT.
- No upstream source files are copied verbatim.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
