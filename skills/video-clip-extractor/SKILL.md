---
name: video-clip-extractor
description: >-
  Extract engaging highlight clips from long videos or livestreams — transcribe with Whisper,
  analyze content to find memorable moments, cut short clips with styled titles and custom cover
  images, and burn subtitles (optionally translated). Use when the user wants to cut the best
  moments from a Bilibili/YouTube URL or a local video file, find highlights from a recording, or
  produce shareable clips with covers. Distinct from vertical-shorts repurposing: this focuses on
  highlight discovery plus title/cover art.
---

# Video clip extractor

Find the moments worth sharing inside a long video or livestream, and package them as finished
clips with titles and covers — not just raw cuts.

## Workflow

1. **Get the source.** Ask for a URL or local file path if missing. For local files with existing
   subtitles, place a matching `.srt` beside the video.
2. **Clarify intent** (optional). If the user wants clips on a specific topic, capture it as the
   selection intent. Otherwise ask once: "Any specific topic or moments to focus on — funny bits,
   key arguments, product reveals?"
3. **Verify the environment.** Check the orchestrator tool is available, ffmpeg is installed, and
   at least one provider key is set. Warn before running if something is missing. Burning subtitles
   needs an ffmpeg build with libass.
4. **Run the extraction** and stream progress to the user. The pipeline transcribes speech,
   analyzes the content against the stated intent, identifies engaging moments, cuts clips, and
   builds titles and cover images.
5. **Report results** — list each generated clip with its source timestamp and title.

## Options worth knowing

| Option | Purpose |
|--------|---------|
| output directory | Where clips are written (default to the user's working folder) |
| max clips | Cap the number of highlights |
| browser choice | Which browser's cookies to use for login-walled sources |
| title style | Visual treatment for the clip title |
| speaker references | Distinguish speakers in multi-person conversations |
| burn subtitles | Embed captions, with optional translation |

## Rules

- Only process content the user has the right to download and clip.
- Use the user's stated intent to guide selection — "engaging" alone is too vague.
- Keep the source timestamps in the report so every clip is traceable to its origin.
- Do not treat automatic scoring as final editorial judgment; offer the user a choice of clips.
- Never publish clips automatically — the user reviews and posts.
- If a provider key is missing, say so before running rather than failing mid-pipeline.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `video-clip-extractor` from
linzzzzzz/openclip. The referenced orchestrator script and coverage of Bilibili/YouTube are from
that project; the script is external and not bundled here.

- Source: https://github.com/linzzzzzz/openclip/tree/main/.claude/skills/video-clip-extractor
- License: MIT — Copyright (c) 2025 OpenClip Contributors.
- No upstream source files are copied verbatim.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
