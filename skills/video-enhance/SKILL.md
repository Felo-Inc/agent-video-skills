---
name: video-enhance
description: >-
  Enhance, upscale, restore and repair existing video — denoise, deblur, deinterlace, stabilize,
  upscale to 4K, frame-interpolate for slow motion, colorize, SDR→HDR — through an enhancement
  provider's API. Use when a clip is soft, noisy, compressed, low-res or flickery and needs a
  finishing pass, or when building a generate-low-res-then-upscale delivery pipeline. Not for
  originating new video or for editorial cuts.
---

# Video enhancement

Enhancement is a **repair and finishing** operation, not a creation operation. It cannot add
information that was never plausibly there — it reconstructs, interpolates, or invents detail.
Every model trades some fidelity for apparent quality; the discipline is choosing the trade that
matches the footage and the deliverable.

## When it applies

- Upscaling (SD→HD, HD→4K/8K) and cleaning AI-generated video that came out soft or flickery.
- Restoring archival footage: grain, compression, interlacing, low resolution.
- Denoise, sharpen, deblur, deinterlace, stabilize, frame-rate conversion, slow motion.
- SDR→HDR, black-and-white colorization, foreground removal.

Not for generating original video, for non-provider upscalers, for editorial decisions, or for
footage already at delivery quality — there, enhancement only adds cost and artifact risk.

## Where enhancement fits

1. **Generate low-res** (e.g. 480–720p) for iteration speed and cost; lock edit, motion, composition.
2. **Enhance/upscale last** to delivery resolution, choosing the model by what the footage needs —
   not by the biggest number.
3. **QA the motion, not just a frame.** Generated video fails temporally: shimmer, warping, identity
   drift. A still can look perfect while the clip is unusable.

Fix temporal warping and noise **before** upscaling — upscaling amplifies both. Separate concerns
into passes (denoise, then upscale, then interpolate), each solving one problem.

## Choosing a model by problem

| Footage problem | Model family |
|-----------------|--------------|
| Low-res AI video, needs faithfulness | precise / realism-oriented upscaler |
| Low-res AI video, want stylized detail | creative / diffusion upscaler (costly, identity risk) |
| Compressed phone / social UGC | general upscale workhorse; face-recovery variant for faces |
| Old archival / film | restoration model; face-recovery for degraded portraits |
| Interlaced broadcast | deinterlace-oriented variant |
| Slow motion / fps change | frame-interpolation model |
| Just noisy | dedicated denoise model |

Model codes, parameters, limits and prices are volatile. Confirm them against the provider's live
reference before hard-coding a pipeline — do not trust cached names.

## API lifecycle (typical)

Enhancement APIs are async, multi-step jobs:

1. **Create** the request with source/output specs and filters — usually free to create, charged
   when processing starts.
2. **Accept** to obtain upload URLs.
3. **Upload** the file, keeping the returned part identifiers.
4. **Complete upload** to start processing.
5. **Poll status** until done, then download.

Use HTTPS and the provider's key header on every call; apply exponential backoff on rate limits;
segment sources over the size cap. Announce the estimated credit cost and wait for approval before
a paid job. Enhance only what you ship — creative models can cost many times a deterministic pass;
prototype settings on a short clip first.

## When enhancement hurts

- **Over-smoothing / waxy faces** — from over-sharpening or heavy denoise. Add a little grain back.
- **Temporal shimmer / warping** — the source is unstable; fix motion first.
- **Face hallucination** — diffusion models invent facial detail; disqualifying for identity-sensitive
  or evidentiary footage.
- **Wasted cost** — source already meets delivery specs.

After any pass, watch the whole clip and check resolution, frame rate, audio passthrough and
artifacts against the brief.

## Rights and provenance

Only enhance footage you have the right to process — API paths upload frames to a third party.
For archival or third-party footage, confirm licensing first. For journalistic, evidentiary or
identity-sensitive material, avoid models that invent detail and disclose that AI enhancement was
applied.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `topaz-video-enhancement` from
calesthio/generative-media-skills. Specific providers, model codes and prices are intentionally
generalized; no provider is endorsed.

- Source: https://github.com/calesthio/generative-media-skills/tree/main/skills/providers/video-enhancement/topaz-video-enhancement
- License: MIT — Copyright (c) 2026 generative-media-skills contributors.
- No upstream source files are copied verbatim.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
