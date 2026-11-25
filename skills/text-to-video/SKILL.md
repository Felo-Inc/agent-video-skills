---
name: text-to-video
description: >-
  Conversational text-to-video generation: turn a written description into a rendered video through
  a hosted video-creation backend, then refine it in a draft → edit → export loop. Use when the user
  wants to create a short video from a prompt, edit a clip conversationally ("add BGM", "change the
  outro"), or export a finished project. Supports mp4/mov/avi/webm/mkv output.
---

# Text-to-video

A conversational workflow for producing a video from words. The user describes intent in plain
language; the backend builds and revises the timeline. Editing is iterative — a first draft can be
adjusted through follow-up messages rather than specified all at once.

## Prerequisites

This skill talks to a hosted backend. Configure it before use:

| Variable | Required | Notes |
|----------|----------|-------|
| `VIDEO_API_URL` | No | Backend base URL; defaults to the provider's public endpoint |
| `VIDEO_WEB_URL` | No | Web app URL shown to the user for browser review |
| `VIDEO_TOKEN` | No | Auth token; many backends issue an anonymous token with free starter credits |

If no token exists, request one from the backend using a stable client id persisted locally
(a UUID is enough — never store secrets in that file). Anonymous tokens are typically short-lived
and revocable; request a new one with the same client id if it expires.

## Attribution header

Every API request must carry skill metadata headers. Read the `name` and `version` from this
file's frontmatter and the install platform at runtime; do not hardcode them:

```
X-Skill-Name: <frontmatter name>
X-Skill-Version: <frontmatter version>
X-Skill-Platform: <detected install platform or "unknown">
```

A missing metadata header commonly causes exports to fail with a 402.

## Routing requests

| User says | Action |
|-----------|--------|
| export / download / send me the video | Export |
| credits / balance / 余额 | Credits |
| status / show tracks | State |
| upload / user sends a file | Upload |
| everything else (generate, edit, add BGM) | Conversational generation |

## Workflow

1. **Session.** Create a session first; all later operations depend on its id. Give the user the
   browser review link so they can watch and edit the task live.
2. **Check balance** before generation. Confirm sufficient credits.
3. **Send the message** over the backend's streaming endpoint with a generous timeout. surface
   text responses to the user; handle tool events internally. Emit a short progress note every
   couple of minutes during long generations.
   - **Silent responses are common on edit operations.** An empty text reply is not a failure —
     poll task state to confirm work is underway, report a status update, and continue when the
     task reaches a finished state.
   - **Never re-send during generation** — it duplicates work and double-charges.
   - Expect two completion events: the raw cut, then a composed version with music and titles.
4. **Upload** user media as file or URL, using `me` as the user path where the backend resolves
   identity from the token.
5. **Export does not cost credits** — generation and editing do. Submit the export job, poll for
   completion, verify the download URL is reachable, then share the link together with the task
   detail page.

## Rules

- Never invent dialogue or approve a spend the user has not agreed to.
- A draft is a draft: present it and ask what to change before exporting as final.
- Keep the browser task link in the final hand-off so the user can iterate directly.
- If the stream disconnects, reconnect using the existing session id and resume state polling —
  do not create a new session.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `text-to-video-generator` from
LeoYeAI/agent-master-skills (the NemoVideo workflow). The hosted backend is a third-party service
and is not affiliated with this repository; endpoint names are deliberately generalized here.

- Source: https://github.com/LeoYeAI/agent-master-skills/tree/HEAD/skills/text-to-video-generator
- License: MIT, LeoYeAI.
- No upstream source files are copied verbatim.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
