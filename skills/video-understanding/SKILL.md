---
name: video-understanding
description: >-
  Turn a long video into a structured understanding index: scene boundaries, ASR transcript,
  per-scene visual observations, silence windows, a fused timeline and a writing brief. Use when
  the user wants to analyze, recap or summarize a video, index a video archive by scene, or prepare
  facts for a narration script. Requires ffmpeg, Python and access to ASR/VLM providers.
---

# Video understanding index

Build a scene-level index of a video so an agent can work from facts instead of guessing. The
pipeline produces a set of files that later stages read:

- `scenes.json` — cut points, with junk segments filtered out.
- `transcript` — dialogue from ASR, with an evidence sidecar documenting timing precision and text
  corrections.
- `observations` — representative frames per scene described by a vision-language model, including
  deeper analysis and frame facts.
- `silence` — windows with no speech.
- `timeline_fusion.json` — everything fused onto one timeline.
- `brief.md` — a short document the agent reads first.

## Roles

Think of this skill as an **observer and script supervisor**, not a storyteller. Facts are kept
separate from inference. Uncertainty is preserved rather than inventing drama. Do not turn an
observation into a claim the video does not support.

## Workflow

1. **Detect scenes** into scene candidates; drop segments too short or too noisy to be useful.
2. **Extract frames** — a few representative frames per kept scene.
3. **Describe visually** — run a vision-language model over the frames for per-scene observations
   and any explicit frame facts. Feed context such as show or character names so the model uses the
   right labels; without it, names will be guessed wrong.
4. **Transcribe** with ASR when there is speech. Pass a vocabulary hint for names and technical
   terms. Keep the evidence sidecar: what was corrected and how precise the timings are. For a
   mostly silent clip, skip ASR and build the timeline from visual observations plus silence windows.
5. **Detect silence windows** and note them — they matter for pacing and edit decisions.
6. **Fuse** all sources onto one timeline, keeping each source's provenance.
7. **Write the brief** the agent reads first: what the video shows, in what order, with timestamps
   and open uncertainties.

## Rules

- **Facts and inference stay separate.** A scene description is a fact; "the creator is building
  toward X" is an inference and must be labelled.
- **Never invent** dialogue, names, motives or outcomes to make a summary livelier.
- **Cache intermediate artifacts** by input and settings so a settings change only recomputes
  affected stages; offer a force option to recompute everything.
- **Do not claim real-time understanding** — this is an offline analysis of a supplied file.
- **Respect source material** — if a frame is unreadable, say so rather than guessing its text.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `video-understanding` from
zenstory-ai/video-recap-skills. The referenced scripts and model providers are external and are not
bundled here.

- Source: https://github.com/zenstory-ai/video-recap-skills/tree/HEAD/skills/video-understanding
- License: MIT — Copyright (c) 2026 PiteChen.
- No upstream source files are copied verbatim.
