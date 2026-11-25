---
name: ai-avatar
description: >-
  Create an AI avatar or talking head of yourself (or a consenting person) — a digital twin that
  looks like them and speaks lines they never recorded in their own cloned voice, lip-synced from
  an audio file. Use when someone wants a digital twin, an AI avatar, a talking photo, or wants
  their avatar to speak in their own voice. Requires an avatar provider (e.g. HeyGen) and a voice
  cloning provider (e.g. ElevenLabs); both are third-party paid services.
---

# AI avatar

An avatar of a person is three independent things, each from its best source:

- **Face and movement** — a digital twin trained from that person's own footage.
- **Voice** — a clone of that person's voice, rendered into an audio file.
- **Lip-sync** — one engine that binds the audio to the face.

**Keep the three apart and only ever change one at a time.** The twin is trained once. The voice
is a file you listen to before it goes anywhere. A render is the twin plus that file on one
engine. When something looks wrong, you can say which part to fix.

## Boundary and consent

- Use this only when the person on screen is the person who consented. Training a likeness or
  cloning a voice of anyone without their explicit agreement is not acceptable.
- A photo-based avatar has no built-in consent check — the responsibility is yours.
- Never add someone else's footage to a person's training group.

## Routes to an avatar

| Route | Input | Cost profile | Best for |
|-------|-------|--------------|----------|
| Digital twin | 15 s–10 min of footage (~2 min ideal) | Training fee, then per render | Anything that must pass as the real person |
| Photo avatar | One photo | Per render, no training | A presenter from a portrait |
| Talking photo | One photo + audio | Cheapest | A single quick line |

## Workflow

1. **Pick the footage** (twin route). Best talking takes: one person, facing camera, face in frame
   throughout, quiet room, 1080p or better, roughly two to three minutes of natural speech.
   Eye-contact takes work best. Download each source once and join locally — never loop ffmpeg
   over a signed URL.
2. **Upload** the footage to the avatar provider and keep the returned asset id beside the file.
3. **Train** — announce the training price and which wallet/account will be charged, then wait for
   a typed yes. A new twin typically issues a consent link the person must complete (often within
   24 hours). Render only once the look is ready and consent is accepted.
4. **Make the line** in the voice provider: about 25 words, 8–10 seconds. Listen to the file and
   verify the words before it goes anywhere.
5. **Render.** Feed the audio into the avatar as an audio asset/URL, not as text plus a voice id —
   cross-provider voice ids do not transfer. Render the same line on each engine you compare; a
   different line hides what the engine did. Announce the price before each paid call and wait for
   approval.
6. **Judge by the mouth.** In a full frame every engine looks fine. Crop the nose-to-chin box at
   several matching moments in each render and in the real footage, stack them, and compare lip
   stretch, teeth shown, lip colour and mouth corners. Show the person both before naming a pick —
   it is their face.
7. **Record the choices** — look id, group, voice and engine — so the result is reproducible.

## Rules

- **Check face-to-voice pairing before every render.** Name files after their person and verify the
  look's name — swapped ids produce a plausible video of the wrong voice.
- **Use a fresh idempotency key per render**, or the provider may return the previous video.
- **Fix an over-acting mouth by changing the engine, not the prompt.** Motion prompts and blink
  tweaks rarely help; a different engine usually does.
- **A calm read beats an acted one.** Start with the default delivery; add emotion only after the
  face is right.
- **A twin is no sharper than its footage.** Train from 1080p; 720p sources yield 720p looks.
- **Announce price and wallet before every paid call** and act only on a typed yes.
- **Watch the whole frame once** — hand gestures can look wrong even when the mouth is fine.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `create-ai-avatar` from
MengTo/Skills. The specific providers, engines, prices and scripts are third-party and are not
bundled or endorsed here.

- Source: https://github.com/MengTo/Skills/tree/main/agent-skills/media/create-ai-avatar
- License: MIT — Copyright (c) 2026 Meng To.
- No upstream source files are copied verbatim.
