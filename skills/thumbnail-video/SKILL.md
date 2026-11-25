---
name: thumbnail-video
description: >-
  Generate YouTube thumbnail variants (1280×720 JPEG) from a video: pick frames via scene
  detection, overlay caption text rendered with HTML/CSS in headless Chrome, and output several
  distinct styles for A/B testing. Use when the user says "make a thumbnail", "generate
  thumbnails", "thumbnail for this video", or any variant of "youtube thumbnail".
---

# Thumbnail from video

Produce N thumbnail variants (1280×720 JPEG, under 2 MB) from a source video. Frames come from
scene detection; typography comes from HTML/CSS templates rendered in headless Chrome. Default to
three variants — matching the usual A/B test cap — and make them meaningfully different designs,
not near-duplicates.

## Prerequisites

Verify `ffmpeg`, `ffprobe`, `python3` and Chrome/Chromium are available before running. Templates
load web fonts at render time, so Chrome needs network access or text falls back to system fonts.
A transcript beside the video is used for hook copy; if none exists, transcribe first.

## Inputs

- Source video path (ask if missing).
- Variant count (default 3, cap 5).
- Optional locked style, hook text override, transcript path.

## Workflow

### 1. Probe and plan

Read the video duration. Decide the variant matrix — for three variants, pick three different
styles. A good default trio:

1. **bold-left** — huge text on one side, frame on the other; benefit/promise tone.
2. **face-zoom** — full-bleed frame, big bottom text; curiosity/question tone.
3. **ui-callout** — UI screenshot, badge and bottom label band; feature-launch tone.

Swap `face-zoom` for a `split-top` tutorial layout when there is no presenter face.

### 2. Extract candidate frames

Run the candidate extractor. It produces scene-change candidates, uniform fallback samples, and
an ordered list with timestamps and paths.

### 3. Draft variants — do not render yet

For each variant:

- **Pick a frame** by viewing candidates. Match frame to style: clean frame with negative space
  for text-driven layouts; a presenter face for face-zoom; the clearest UI shot for callouts;
  the most evocative frame for minimal.
- **Generate a hook** from the style's pattern and word cap: benefit ("Sync once. Use everywhere."),
  question ("Still deploying manually?"), curiosity ("The button that changes everything"),
  feature ("NEW: Web-managed profiles") or tutorial. Pull vocabulary from the transcript. Avoid
  clickbait the user would not say.
- **Subhook** if the style supports one — a small second line for context.

### 4. Present the plan and get sign-off

Show a compact table of variants: style, hook, subhook and frame timestamp. Then ask, in one call:

1. Approve the plan — render as drafted / change hooks / change frames or styles.
2. Color treatment — default per style / a single bold accent / brand colors if known.

If the user chooses changes, iterate and re-ask. Only render after approval. Map color choices to
the template's accent/text/background variables.

### 5. Render

Render each variant: substitute the template, screenshot at 1280×720 in headless Chrome, convert to
JPEG at quality 90, and verify the file is under 2 MB.

### 6. Deliver

Write variants next to the source video with clear filenames, and report the styles, hooks and
frame timestamps used so the user can reproduce or tweak them.

## Rules

- Never render before the plan is approved — thumbnails are a design decision.
- Keep the three variants genuinely different so the A/B test is meaningful.
- Do not invent a face or misrepresent a product; use only frames from the supplied video.
- A missing transcript is not a reason to invent hook claims — ask or transcribe.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `thumbnail-video` from
smitmartijn/claude-skills. The referenced scripts, templates and styles are external and are not
bundled here.

- Source: https://github.com/smitmartijn/claude-skills/tree/HEAD/thumbnail-video
- License: MIT — Copyright (c) 2026 Martijn Smit.
- No upstream source files are copied verbatim.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
