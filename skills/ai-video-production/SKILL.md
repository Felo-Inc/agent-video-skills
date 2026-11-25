---
name: ai-video-production
description: >-
  End-to-end production of AI-assisted narrated explainer videos and lyric-synced music videos for
  a solo creator: script, storyboard with a decision log, voiceover generation and ASR verification,
  shot timing tied to the voiceover, Remotion motion graphics, and publishing. Use when the user
  wants to write, storyboard, voice, animate, render or revise an explainer, tutorial, news video
  or music video. Triggers: 写脚本, 分镜, 配音, 动画, 动态图形, 视觉语言, 音乐 MV, 做视频.
---

# AI video production

A pipeline for one person making narrated explainer videos (and song music videos) with AI tools.
Every stage writes files the next stage reads, so any stage can be redone without breaking the rest.

```
Script.md → generate voiceover → verify by ASR → assemble timeline + SRT
        → Storyboard.md (decision log) → Remotion project → draft MP4 → final
```

## Rules that matter most

1. **The voiceover drives the timing.** Write the script, generate the VO, then time shots to it —
   never the reverse. Animation cues hang off sentence times, so re-recording a line moves the
   picture with it.
2. **TTS one whole sentence at a time.** Never split at commas. Each sentence is one file, grouped
   in a folder per shot. Fragmented reads sound slow and robotic.
3. **Every VO line is checked by ear or ASR.** Character-voice TTS silently drops words.
   Transcribe each line, re-synthesize flagged ones, rewrite a sentence that keeps failing.
4. **One visual language per video** (at most one accent). The storyboard's *visual style / look*
   field names it and the renderer follows it.
5. **The storyboard is the project's memory.** It holds locked decisions, a shot list, a decision
   log (date, scope, decision, reason, decided by) and open questions. Your proposals stay marked
   待确认 / proposed until the creator confirms them. Never build on an unconfirmed proposal.
6. **Real sources only.** News visuals use real posts, shown faithfully with original media. A
   deleted post is labelled deleted, never reconstructed. Every factual claim has a source.
7. **Match the creator's voice.** A solo creator narrates as 我, not 我们. Ask once and record it.
8. **Previs before generation.** Block the shot in the project's own renderer, export its still,
   then hand that still to a video model only for shots the engine is weak at (faces, crowds,
   cloth, photoreal machines). The deterministic render stays the master; generated footage is an
   added layer, and every generated shot is logged with tool, reference still and seed.
9. **Every cover ships in two ratios** — 16:9 (1920×1080) and 4:3 (1440×1080), same design from
   the same motion project, if the destination platform requires both.
10. **Publishing needs an explicit gate per upload** unless the creator has given standing
    authorization. Never touch a credential vault.

## Stage checklist

| Stage | Output |
|-------|--------|
| Script | Logline, scenes, VISUAL / VO / MUSIC-SFX blocks, `[S#-##]` shot tags on VO lines, sources |
| Storyboard | Locked aspect, visual language, palette, pacing, typography, recurring props, shot list with minimum durations, decision log |
| Previs | One full-size still per shot; composition reviewed and fixed before motion work |
| Voiceover | Engine running → generate per-sentence files → ASR verify → assemble timeline + SRT, write durations back into the shot table |
| Motion | Remotion project from a starter, one component per shot, synced to the VO timeline, contact-sheet stills |
| Social cards | Real posts shown with original text first, then a translation covering it |
| Review | Creator watches the draft; every change logged; VO / draft version bumped |
| Publish | Covers in required ratios + upload metadata; upload only with the creator's approval |

For music videos: analyze song tempo/key/sections, force-align lyric timings to official lyric
text, pick a palette with the creator, storyboard per line with a new scene for every repeated
line, render frame-pure, run a text audit, then mux. Do not share graphics with another video.

## Working habits

- **Version, don't overwrite:** `VO v1` → `VO v2`, `title_draft_v1.mp4` → `_v2`.
- **Review with contact sheets first**, then a short frame range, then the full draft.
- Before changing a pronunciation or style rule, make short A/B clips or stills and let the
  creator choose.
- **Copyright:** mute embedded third-party video audio with background music (content ID flags);
  generate SFX in code; credit CC-BY assets.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `ai-video-production` from
Catnip202X/ai-video-production. Its TTS engines, Remotion starter and publishing MCP are external
tools and are not bundled here.

- Source: https://github.com/Catnip202X/ai-video-production
- License: MIT — Copyright (c) 2026 Catnip202X. Bundled third-party pieces in the upstream project
  keep their own terms; review them before reuse.
- No upstream source files are copied verbatim.
