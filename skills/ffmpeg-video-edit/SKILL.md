---
name: ffmpeg-video-edit
description: >-
  Edit video and audio with local FFmpeg through a contract-driven tool set: cut, join, reframe,
  speed, captions, overlays, silence removal, sync, loudness, HDR-to-SDR, platform exports and
  delivery checks. Use whenever the user mentions a video or audio file (mp4, mov, wav, m4a),
  footage, captions, a reel or short, YouTube/TikTok delivery, LUFS or ffmpeg — even without saying
  "edit". Needs FFmpeg 6.1+ and Python 3.10+; standard library only, no cloud, no API keys.
---

# FFmpeg video editing

Run a tool as `python3 <skill-dir>/scripts/<name>.py`; `--help` lists every flag. Tools expose a
machine-readable contract: `contract --json` lists inputs, outputs, required FFmpeg components and
verification steps.

## Prerequisites

- FFmpeg 6.1+ and ffprobe on `PATH` (`ffmpeg -version`). Verify components such as `libx264`,
  `subtitles`, `loudnorm` with the tool's `doctor` command.
- Python 3.10+, standard library only.

## Core conventions

- **Shared flags:** `--dry-run` (plan, write nothing), `--json` (structured output + probe +
  commands), `--json-brief` (status + summary), `--overwrite` (allow replacing existing output),
  `--timeout SECONDS` (default 1800). Writing tools do nothing under `--dry-run`; measuring tools
  may still run ffmpeg/ffprobe without writing artifacts.
- **One ordinary edit is one call.** A writing tool reads its own input, refuses what it cannot do
  (the error says what to change) and verifies what it wrote. Run it with `--json` and report from
  its document: `wrote`, a human summary (length and any miss against the request), and `verified`.
- For a cut, resize, pad, rotation, speed, format or sound change, do **not** probe first, plan with
  `--dry-run`, re-probe, or read `--help` when the routing table gives the command.
- Audio tools accept audio-only files (including `.mka`); picture tools require video.

## Routing

| Intent | Tool family |
|--------|-------------|
| Inspect a file / stream info | `probe` |
| Cut, join, fit to duration or aspect, pad | `cut`, `fit`, `join` |
| Silence removal, loudness, audio cleanup | `silence`, `loudness` |
| Captions, text/graphics overlays | `caption`, `overlay` |
| Scene detection, highlight reels, contact sheets | `scenes`, `sheet` |
| HDR/Dolby Vision → SDR, LUT/color | `color`, `hdr` |
| Sync / multicam / external mic | `sync`, `multicam` |
| Platform export and delivery check | `export`, `check` |
| Batch processing / repeatable project | `batch`, `render` |

Run `contract --json` to get the exact tool names and parameter schemas exposed by the installed
version; do not guess flags.

## Decision boundaries

This skill **executes** an edit; it does not decide one. These choices belong to the human, the
calling agent or another skill:

- Which cut is right, and whether a deliverable is approvable — this skill measures and reports.
- What makes a highlight interesting — ranking is a measured proxy, not editorial judgment.
- Thumbnail / cover composition and what a video is *about*.
- Whether something "looks good" — a LUT is mechanical; aesthetic grading is a separate decision.
- The words in a caption — burned exactly as written; never rewrite or shorten to "make it fit".
- A subject or crop region that was not provided — the calling agent decides from a contact sheet.

## Rules

- **Destination** sets aspect, length, loudness and codec. "Export/post/deliver" with none named →
  ask.
- **Duration** without a method → decide what to keep first. Drop dead air (`silence`) and unwanted
  spans, or trim for a simple cut; retime only when asked. A large implicit retime fails with
  `fit_method_required`.
- **Captions without text** → transcribe if a local speech engine exists (name the spoken
  language); otherwise ask. Never invent dialogue.
- Anything else: pick the conventional default, say what you picked, offer the alternative in one
  line.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `ffmpeg-skill` from
kajisho5/ffmpeg-skill. Its 40+ scripts and MCP server are external tools and are not bundled here.

- Source: https://github.com/kajisho5/ffmpeg-skill
- License: MIT, kajisho5.
- No upstream source files are copied verbatim. `references/` and `scripts/` from upstream are not
  redistributed; install them from the source project if needed.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
