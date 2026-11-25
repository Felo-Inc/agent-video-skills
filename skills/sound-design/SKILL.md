---
name: sound-design
description: >-
  Think like a professional video editor about sound: read the footage or script, split it into
  moments, choose which sound layers fit each one (music, SFX, transition, ambience, foley, stings,
  UI sounds), then generate the audio assets via an API or local synthesis. Use when planning or
  reviewing a video's sound design, or asked to "generate a whoosh for this cut" / "suggest and
  create SFX for this scene". Not for voice-over narration or mixing audio into the final video.
---

# Sound design

Good sound is chosen moment by moment, not poured from a template. This skill decides **which**
sound layers fit **which** moments of an edit, then generates the audio assets.

## The eight sound types

| Type | Role |
|------|------|
| Background music | Overall emotional tone, runs under the video |
| Sound effect (SFX) | Feedback for a specific visible action or object |
| Transition sound | Bridges a cut — whoosh, riser, impact, braam |
| Ambience | Establishes a real physical space (room tone) |
| Voice-over / dialogue | Primary spoken content — top priority layer |
| Jingle / sting | Short brand-recognition sound at open/close |
| Foley | Sound precisely synced to an on-screen movement |
| UI sound | Feedback for on-screen text, elements, notifications |

## Core process

1. **Gather source material** — script, transcript, timeline export, or the user's description.
2. **Split into moments.** Always do this before choosing any sound. For each moment record the
   signals: dialogue, action, cut type, branding, mood. Skipping this step produces generic,
   template-driven choices.
3. **Choose the primary sound type** per moment using a question-based framework (what happens on
   screen → which sound fits), then cross-check against the video's overall genre palette.
4. **Sanity-check across all moments** for common mistakes: music fighting voice-over, missing SFX
   on visible actions, overused transitions, competing layers.
5. **Record precise placement** — a timestamp or sync point, not "somewhere in this scene". A
   recommendation without placement is not actionable.
6. **Confirm the generation mode with the user** before producing audio: API-based (best quality,
   needs keys) or local Python synthesis (no key, lower quality ceiling); and whether to run it
   directly or delegate the script. Never generate silently or assume what is configured.
7. **Generate at WAV / 48 kHz**, respect the layering priority so layers duck under voice, verify
   each file exists, then report paths and placements.

## Layering priority

Voice-over and dialogue always outrank music and ambience. When two layers compete, state how they
duck or coexist. Route melodic requests (BGM, melodic jingles) to a music-capable backend — not to
an SFX generator that can only make non-melodic hits. If using local synthesis, state its quality
ceiling honestly rather than presenting it as equivalent to API output.

## Rules

- Every recommendation must be justified by a specific on-screen cue, not a genre default.
- No more than one competing layer per moment without a ducking note.
- Voice-over generation and final audio mixing are out of scope — this skill produces sound assets
  and placement recommendations.
- Confirm any extra dependencies (numpy, scipy, MIDI/FluidSynth, SoundFont) are available before
  writing code that assumes them.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `sound-generation` from
dodoxtech/sonic-skill. Its references and generation backends are external and not bundled here.

- Source: https://github.com/dodoxtech/sonic-skill/tree/main/skills/sound-generation
- License: MIT — Copyright (c) 2026 dodoxtech.
- No upstream source files are copied verbatim.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
