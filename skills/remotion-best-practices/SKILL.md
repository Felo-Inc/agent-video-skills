---
name: remotion-best-practices
description: >-
  Domain-knowledge router for Remotion video code. Use whenever writing, reviewing or debugging a
  Remotion project — it points to the precise rule for animation timing, transitions, captions,
  audio, images/video/audio embedding, fonts, charts, 3D, measuring text, calculateMetadata and
  rendering. Load this to avoid inventing Remotion APIs.
---

# Remotion best practices

The `SKILL.md` body is a table of contents; deep rules live in the `rules/` directory of the
installed skill. Read only the rules relevant to the task.

**When to use:** any Remotion code work — building, reviewing or debugging.
**How to use:** read the matching rule file(s) before writing code.

## Rule index

Read `rules/<name>.md` for detail and code examples.

| Need | Rule |
|------|------|
| Fundamental animation techniques | `animations.md` |
| interpolate / spring / easing curves | `timing.md` |
| Scene transitions | `transitions.md` |
| Delay, trim, limit duration | `sequencing.md` |
| Cut beginning or end of animations | `trimming.md` |
| Embed images with `Img` | `images.md` |
| Embed video, trimming, volume, speed, loop, pitch | `videos.md` |
| Audio import, trim, volume, speed, pitch | `audio.md` |
| Display GIFs on the timeline | `gifs.md` |
| Embed Lottie animations | `lottie.md` |
| Google Fonts and local fonts | `fonts.md` |
| Import SRT captions with `@remotion/captions` | `import-srt-captions.md` |
| Transcribe audio into captions | `transcribe-captions.md` |
| TikTok-style word highlighting | `display-captions.md` |
| Dynamic duration, dimensions, props | `calculate-metadata.md` |
| Compositions, stills, folders, defaultProps | `compositions.md` |
| Charts and data visualization | `charts.md` |
| Three.js / React Three Fiber 3D | `3d.md` |
| Embedding assets | `assets.md` |
| TailwindCSS in Remotion | `tailwind.md` |
| Typography and text animation | `text-animations.md` |
| Measure text, fit to container, check overflow | `measuring-text.md` |
| Measure DOM node dimensions | `measuring-dom-nodes.md` |
| Can the browser decode this video? (Mediabunny) | `can-decode.md` |
| Extract frames at timestamps (Mediabunny) | `extract-frames.md` |
| Get audio duration | `get-audio-duration.md` |
| Get video duration / dimensions | `get-video-duration.md`, `get-video-dimensions.md` |

## Core guardrails (apply always)

- `.tsx` for JSX; `registerRoot` + `Composition` to register; render by composition name.
- Pass `fps` to `spring()`; obtain it from `useVideoConfig()`.
- All animation derives from `useCurrentFrame()` — never `setInterval` or wall-clock time. Render
  must be deterministic frame by frame.
- Measure text and DOM nodes rather than guessing sizes; overflow checks are explicit.
- Captions: import SRT with `@remotion/captions`; sync word highlights to the current frame.
- External media must be loadable at render time; prefer local assets under `public/`.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `remotion-best-practices` from
Karanjot786/agent-skills-cli. The `rules/` files are external resources of that project and are
not bundled here.

- Source: https://github.com/Karanjot786/agent-skills-cli/tree/HEAD/.agent/skills/remotion-best-practices
- Also inspired by the comparable rule set in affaan-m/ecc (`remotion-video-creation`) and
  jdrhyne/agent-skills (`remotion`), both MIT.
- License: MIT.
- No upstream source files are copied verbatim.
