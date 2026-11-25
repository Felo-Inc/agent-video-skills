---
name: seedance-video
description: >-
  Plan, prompt and render Seedance 2.5 / 2.0 videos. Use when the user wants a Seedance prompt,
  a multi-shot story, ad or explainer made with Seedance, or wants the video itself rendered.
  Writes prompts following the BytePlus Seedance guide, plans shots, quotes credit cost before
  spending, renders cheap drafts, chains shots from the previous last frame, and only renders
  1080p finals after approval.
---

# Seedance video

Turn an idea into Seedance prompts and, when a Seedance MCP server is connected, into rendered
clips.

## Two modes

- **Render mode** — video tools (`quote_video`, `create_video`, `get_video`, `render_final`,
  `list_models`, `list_characters`, `generate_image`) are available. Plan, quote, render and
  deliver links.
- **Prompt mode** — those tools are absent. Plan the shots and write prompts and settings, then
  tell the user how to render them. **Never claim a video was rendered unless `get_video`
  returned `succeeded` with a download link.**

## 1. Pin down the brief

Ask at most three short questions, only for what is missing:

- where it will be posted — 9:16 for TikTok/Reels/Shorts, 16:9 for YouTube/web;
- total length and look — live-action, stylized 3D, anime, product studio;
- recurring characters or products, and whether the user has images of them.

If the user says "just go": 9:16, about 5 s per shot, and the look implied by the idea.

## 2. Plan the shots

- **One beat per shot** — one action and at most one line of dialogue. Next beat = next shot.
- Typically 3–6 shots for a short story, 2–4 for a product clip.
- Pick durations/resolutions the model allows; call `list_models` in render mode instead of
  assuming. Seedance 2.5 handles longer shots, omni references, 1080p and draft mode; 2.0 Mini /
  Fast are cheapest for 480p/720p drafts.
- Show the plan as a table before rendering anything:

| # | Seconds | What happens | Camera | Dialogue | Continues from |
|---|---------|--------------|--------|----------|----------------|

## 3. Write each prompt

1. **Open with format:** aspect ratio, length, look — "Vertical 9:16, 5-second shot, stylized 3D animation."
2. **Give every reference one job, by position:** "@image1 is the main character only. Keep face,
   hair and outfit identical." "@video1 is a motion reference — copy the movement, not the person."
3. **Subject + one action**, written as what happens, not as adjectives.
4. **One camera instruction** (push-in, tracking, locked eye-level, whip-pan). Unspecified camera
   is random camera.
5. **Dialogue with the speaker named first:** `MAYA: "We're late."` — say who else stays silent.
6. **End with exclusions** when needed: "No subtitles, no on-screen text."
7. Write prompts in English; keep the conversation in the user's language.

## 4. Keep characters consistent

- Uploaded media with a recognizable **real face is rejected** by the model (nothing charged).
- For a realistic or recurring person, use a verified portrait from `list_characters` (an
  `asset://` reference) or generate a character sheet. `generate_image` is **paid per image** —
  take its price from `list_models`, include it in the quote, and call only after approval.
- Attach the same character references to every shot showing that character; keep restating
  "keep face, hair and outfit identical". Describe action and camera, not the face again.

## 5. Quote first, approve in stages

1. **Quote and estimate.** Call `quote_video` with exact settings for every shot whose inputs
   exist. Estimate the rest from a quoted shot with the same model/duration/resolution/audio, and
   label them as estimates. Character sheets cost the per-image price in `list_models`.
2. Show cost per shot, any image costs and the total, in credits (1 credit = USD 0.01).
3. **Wait for an explicit yes** before any `create_video`, `render_final` or `generate_image`.
4. **Go stage by stage.** Generate approved character sheets first. Before each dependent shot,
   re-quote with exact inputs: render if within the approved amount, otherwise stop and ask.
   Never spend beyond the approved total.
5. With Seedance 2.5 prefer drafts: `create_video` with `draft: true` renders a cheap 480p
   preview; call `render_final` only for approved drafts, before `draft_expires_at`.

## 6. Render and chain

- `create_video`, then poll `get_video` **no more than every 20 s**. Typical jobs take 1–5 min.
- To continue from the previous shot, take `result.last_frame_url` and pass it as the first image
  to an image-to-video model. **Only chain this way when no realistic human face is in frame** —
  a stored last frame is checked like an upload and rejected with `real_person_detected`.
- For a realistic recurring person, use reference-to-video in every shot with the same verified
  portrait or character sheet; do not chain by last frame.
- On failure, credits are released automatically. Read the error: change the prompt for
  `prompt_rejected`, change inputs for `content_rejected` / `real_person_detected`; never resend
  the same request. Media inputs must be public HTTPS URLs.

## 7. Deliver

List finished clips in order with download links (they expire — tell the user to save them).
To join them locally:

```bash
printf "file '%s'\n" shot1.mp4 shot2.mp4 shot3.mp4 > list.txt
ffmpeg -f concat -safe 0 -i list.txt -c copy episode.mp4
```

Offer the next step: another shot, a retake, or a 1080p final of an approved draft.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `seedance-video` from
AiuniVid/seedance-video-skill. The MCP server referenced above is a third-party service and is
not affiliated with this repository.

- Source: https://github.com/AiuniVid/seedance-video-skill
- License: MIT — Copyright (c) 2026 AiuniVid.
- No upstream source files are copied verbatim.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
