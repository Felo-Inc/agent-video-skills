---
name: lipsync
description: >-
  Drive a face's mouth from an audio track — lip-sync a portrait or an existing video to a voice,
  dub a line onto footage, or generate a talking clip from a script. Use when the user asks to
  "lip sync", "make this video speak", "match audio to mouth", "dub video", or "sync lips to
  voice". Routes across lip-sync providers; requires a third-party API key.
---

# Lip sync

A talking clip is two assets that must agree: a **voice** and a **face**. Make the voice first.
The line's length, pacing and emphasis decide the clip; the face is fitted to the audio, not the
other way round. Most failed talking clips are a good face on a line that never fitted it.

## Route by starting point

| Starting point | Route |
|----------------|-------|
| A script, no audio yet | text-to-speech first, then lip-sync |
| An approved still + a line | image-to-video with lip-sync |
| Existing footage + a new line | video lip-sync on the source footage |

Pick the provider endpoint by what the user has: portrait + audio (avatar-style), video + audio
(mouth-swap on existing footage), or generate-and-sync from a script. Read the chosen provider's
capability list before the first run — the catalog and supported languages change.

## Two kinds of lip-sync model

The decision that matters more than voice quality is what happens to length:

- **Keep the picture and its length exactly** — use when the dub goes back over an existing edit,
  a fixed timeline or a fixed-length ad slot.
- **Re-sync the mouth and change length** — use for an on-screen presenter; never for a clip that
  must keep its runtime.

If a line overruns the slot, shorten the copy — do not silently cram or pitch-shift the audio unless
the provider explicitly supports duration-matched generation.

## Workflow

1. **Prepare the voice.** Generate or obtain the audio, listen to it, and confirm the words and
   duration. For brand names and compound terms, add phonetic hints to the script rather than
   trusting default pronunciation.
2. **Choose the route** from the table and confirm the input asset (still, video or script).
3. **Quote, then render.** Announce the cost and wait for approval before any paid call. Attach
   the media in the input slot the provider documents — do not assume a field name.
4. **Poll to completion** at the documented interval; on failure, read the error and change the
   input or route rather than resending blindly.
5. **Verify** mouth/audio agreement at several points, and that the clip length still matches the
   intended slot. Deliver the file path and report voice, language and any duration mismatch.

## Rules

- A recognizable real person's likeness or voice requires their consent.
- Use the same audio when comparing engines — a new line hides what the engine did.
- Do not invent dialogue. Only sync words the user supplied or that a transcript produced.
- Do not loop retries on a paid endpoint; each attempt can be billed.
- If sync drifts or a voice changes between shots, keep the same voice/settings across the set.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** the `lipsync` skill from
genmedia-labs/skills and `layer-talking-characters` from layerai/skills, both MIT. Specific provider
names and endpoints are intentionally generalized.

- Sources:
  - https://github.com/genmedia-labs/skills/tree/main/lipsync
  - https://github.com/layerai/skills/tree/main/plugins/layer/skills/layer-talking-characters
- License: MIT.
- No upstream source files are copied verbatim.
