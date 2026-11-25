---
name: video-localization
description: >-
  Ship one approved video asset in several languages: dub the voice, burn per-market subtitles,
  or translate text baked into an image, end card or UI. Use when the user wants to localize,
  localise, dub, translate a video, add multilingual captions, or fix a dub that drifted out of
  sync or a translated line that no longer fits. Requires a third-party dubbing/caption provider.
---

# Video localization

Localization is **one approved master multiplied by a list of languages**. Every language version
comes from the master — never from another language's version. A German cut made from the French
cut carries the French cut's defects into German.

Three layers of an asset may need work:

- **Voice** — dub an existing video, or speak a translated script with text-to-speech.
- **Captions** — burn subtitles per market.
- **Text in images** — replace baked-in words, or letter a clean plate per language.

## Plan the matrix first

Before any paid run, write the matrix: each master `asset_id`, each language code, and an empty
cell for each output. Language codes (e.g. `de`, `ja`, `pt`) name a language, not a market — if the
user needs Brazilian rather than European Portuguese, say a code alone may not distinguish them
and check the provider's list.

Get approved translations from the user or their vendor. If you translate copy yourself, label it
a **draft for review** — store copy, legal lines and character names are the user's call. Price the
whole matrix before the first run and apply a spend gate to the total. Text-to-speech is usually
priced per character, so each language's script is its own estimate.

## Voice

**Dubbing** keeps the original performance and changes its language. Choose models that preserve
picture length when the dub goes over an existing edit or a fixed ad slot; choose lip-resyncing
models for an on-screen presenter — never for a clip that must keep its runtime.

**Text-to-speech** suits a fresh voice-over from a translated script. Set the speech language when
lines are short or full of names and loanwords — exactly what a model reads in the wrong language.
Reuse the same voice choices across a language's lines so a character does not change voice
mid-campaign.

Translated speech runs longer. German and French often outgrow English; a 15-second slot does not
stretch. **Shorten the line, not the pacing** — a small speed nudge is fine, a crammed read is not.

## Captions

Spell style presets exactly as the provider lists them. Dynamic presets animate word by word and
usually cost more — pass the same preset to the estimate. Caption each language's dub, not the
master, and confirm the model supports that language. Burned-in captions produce one file per
language, so always keep a clean master. Move captions to the top when the lower third carries a
CTA, gameplay UI or a title.

## Text in images

The cheapest localization is art with no words baked in: generate a clean master and letter each
language separately. When words are baked into a frame, either run an edit-text model with the
exact replacement string, or erase the text to a clean plate and letter that plate per language.

- **Script coverage:** a Latin brand font usually lacks CJK, Cyrillic, Thai or Arabic glyphs;
  missing glyphs render as empty boxes. Use a family that covers the script and inspect every render.
- **Direction and shaping:** for RTL and joined scripts, verify visually that letters join and run
  in the right direction; if not, report it rather than ship.
- **Expansion:** size the text box for the longest language and render every language into the same
  box. Shorten copy or lower font size **consistently across the set** — never let one market's
  title be visibly smaller.

## Workflow

1. Write the master × language matrix and clarify market variants.
2. List candidate models/endpoints for each job and read capabilities before the first run.
3. Estimate the whole matrix; present the total and wait for explicit approval above the gate.
4. Execute per language, poll each run, and watch each dub against the picture.
5. Letter clean art per language with a shared box and a script-covering font.
6. Fill the matrix with every output id and hand it over, flagging drafts and mismatches.

## Common mistakes

- Localizing from another language's version instead of the master.
- A lip-resyncing dub dropped into a fixed-length edit.
- Estimating one language and assuming the rest cost the same.
- A brand font lacking the script, shipped with empty boxes.
- Translating store or legal copy and presenting it as final.
- Burning captions into the only copy of the master.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** the `layer-localization` skill from
layerai/skills and the dubbing skill in elevenlabs/skills, both MIT. Provider-specific names and
parameters are generalized.

- Sources:
  - https://github.com/layerai/skills/tree/main/plugins/layer/skills/layer-localization
  - https://github.com/elevenlabs/skills/tree/main/dubbing
- License: MIT — Copyright (c) 2026 Layer AI; Copyright (c) 2024 ElevenLabs.
- No upstream source files are copied verbatim.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
