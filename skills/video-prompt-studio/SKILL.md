---
name: video-prompt-studio
description: >-
  Turn a rough idea into a structured, model-ready video prompt. Use when the user wants a
  video prompt, a shot description, a storyboard beat, or wants to plan an AI video before
  generating it. Produces a JSON prompt covering scene, characters, camera, dialogue and audio,
  and optionally binds a reference image. Works with any text-to-video model that accepts
  descriptive prompts.
  Trigger phrases: "video prompt", "write a prompt for a video", "plan this video clip",
  "storyboard this scene", "做视频提示词", "写视频分镜".
---

# Video Prompt Studio

Turn a one-line idea into a precise prompt that a video model can actually execute. A good
prompt describes what happens, not a list of adjectives.

## When to use

- The user has an idea but no prompt.
- A scene needs to be broken into shots before generation.
- A reference image should guide the first or last frame.

## Workflow

### 1. Extract the requirements

Identify, without asking what can be inferred:

- **Subject / content** — who or what is on screen.
- **Style** — art direction, mood, palette, era.
- **Technical** — aspect ratio, shot size, lighting, camera.
- **Reference image** — a supplied image to guide composition or serve as first/last frame.
- **Dialogue / audio** — spoken lines, sound effects, music cue.

Ask at most three short questions, only for genuinely missing essentials such as target platform
(sets aspect ratio) or recurring characters.

### 2. Build the structured prompt

Write a JSON object. Keep every field concrete and visual:

```json
{
  "title": "short descriptive title",
  "background": {
    "description": "what the setting looks like and what is happening in it",
    "era": "time period, if relevant",
    "location": "specific place"
  },
  "characters": ["named subjects and their defining appearance"],
  "camera": {
    "type": "close-up two-shot / wide tracking / top-down ...",
    "movement": "static, slow push-in, handheld, whip-pan ...",
    "angle": "eye-level, low angle, over-the-shoulder ...",
    "focus": "what is sharp and what falls to bokeh"
  },
  "dialogue": [
    { "character": "NAME", "text": "spoken line" }
  ],
  "audio": [
    { "type": "train whistle, distant, rising", "volume": 1 },
    { "type": "strings swell then fade", "volume": 0.5 }
  ]
}
```

### 3. Bind a reference image

If the user supplied one image, treat it as the guiding frame. If two are supplied, treat them
as first and last frame. State explicitly in the prompt what the reference controls —
"keep face, hair and outfit identical" — and what it does not.

### 4. Rules

- Always write prompt content in English, regardless of the user's language. Keep the
  conversation in the user's language.
- One shot = one action and at most one line of dialogue. Split larger scenes into beats.
- Give the camera one instruction. Unspecified camera means a random camera.
- Add exclusions only when needed: "no subtitles, no on-screen text".
- Do not claim a video was rendered. This skill produces prompts; rendering belongs to a
  generation skill or an external tool.
- If a generation tool is available and the user approves, pass the JSON as its prompt input.

## Output

Present the JSON prompt and a one-line plain-language summary of the shot. Offer to split the
scene into more shots or to adjust style before generation.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** the `video-generation` skill in
Citrus-bit/Anaxa.

- Source: https://github.com/Citrus-bit/Anaxa/tree/HEAD/skills/public/video-generation
- License: MIT — Copyright (c) 2025 Bytedance Ltd. and/or its affiliates; 2025-2026 DeerFlow Authors; 2026 MedrixFlow Authors.
- No upstream source files are copied verbatim.
