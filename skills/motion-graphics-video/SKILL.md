---
name: motion-graphics-video
description: >-
  Turn a short brief plus optional screenshots, design references, logo, music, footage or
  voiceover into a directed motion-graphics MP4. Builds HTML/CSS/SVG scenes and renders them
  frame-exact with headless Chromium and ffmpeg, with optional synthesized motion sound effects.
  Use for product teasers, feature explainers, app demos, data stories, social reels, kinetic
  typography and music-synced edits. Not for static images, slide decks or AI-generated live action.
---

# Motion graphics video

**Direct first, then build.** Never turn a plain brief straight into code.

## Tooling

A single CLI drives the workflow, run from the project directory:

```bash
node <skill-dir>/scripts/video.mjs <command> [flags]
```

`<skill-dir>` is the absolute directory this skill was loaded from — never the project directory.
Command flags and setup live in the CLI reference shipped with the tool.

## Workflow

1. **Sweep.** Run `doctor` in the user's folder. Fix every `MISSING` line under `READY`, or tell
   the user. Plan around each `LIMIT`. Plan with what exists: a software-only machine keeps 3D and
   blur light; an English-only voice never narrates another language.
2. **Gather facts** from the user's material first; research only the gaps. Write the facts with
   sources before anything else. Every claim on screen must come from them.
3. **Ask, when it matters.** One question, one message. Skip for a one-shot or unattended run.
4. **Direct.** Run `init` in the user's working directory (never inside `<skill-dir>`). Fill the
   direction file: write three concepts, pick the strongest, choose ratio/size/fps for the
   platform. Give the user a five-line summary and continue without waiting.
5. **Sound.** Voice, music and effects combine as needed. Write the sonic concept and energy arc
   first. Use the user's narration as given; follow the TTS rules for synthesized speech. **Never
   add captions or a subtitle file without the user's yes.** Music only from the user's own track.
   Motion effects on by default; silence on request disables sfx, voice and music.
6. **Build scenes.** Rebuild reference designs as live HTML. Never animate a flat screenshot of a
   design that can be rebuilt.
7. **Check each scene** after writing or editing (`check --scene N`). Open its still sheet, fix
   every finding in one edit, then re-run. A warning stays only for a deliberate choice.
8. **Render.** Run `render --draft` once every scene passes and again after each fix. Run the full
   render once the draft passes review. With a sound bed, compare the no-bed copy.
9. **Review.** The render step already produced the contact sheet and, with effects, the audit
   sheet. Compare each cue's intent with its thumbnail; fix failing cues and mislabeled intents,
   then render again. Listen to the mix when playback is available; report when it was not.
10. **Deliver.** Check the thumbnail, report the master, the compressed copy and the thumbnail,
    and prepare upload copies and listing text.

## Non-negotiables

- One visual language per video: shared type, icon family, light and camera language.
- A concept, not a template — story shape, compositions and copy come from this product.
- Tools supply the craft, not the idea; reference tables show a range, never a menu.
- No dead frame: the content carries the motion. The camera moves only with a reason.
- Screen text holds still while the camera moves the world under it; world text moves with the world.
- Every feature is shown by a verb moment, never a bullet list.
- On-screen text passes `check` for size, contrast and hold time.

## Boundaries

- Static designs need a design tool; slide decks need a slides tool.
- Charts inside a video: one message per chart, the right chart form, meaningful color.
- Live-action footage is composed from supplied footage, never generated here.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `motion-video` from
farhan-syah/motion-video-skill. The referenced CLI, its scripts and reference tables are external
tools and are not bundled here.

- Source: https://github.com/farhan-syah/motion-video-skill
- License: MIT, farhan-syah.
- No upstream source files are copied verbatim.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
