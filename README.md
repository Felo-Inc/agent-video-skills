<p align="center">
  <img src="assets/meltica-logo.svg#gh-light-mode-only" alt="Meltica" width="260">
  <img src="assets/meltica-logo-dark.svg#gh-dark-mode-only" alt="Meltica" width="260">
</p>

<p align="center">
  <strong>Built by the team behind <a href="https://meltica.ai">Meltica</a></strong> — an AI promo-video platform for products, apps and local businesses.
  <br>Never wonder what to post again: turn an idea or a reference into a short-video plan you can review and publish.
</p>

<p align="center">
  <a href="https://meltica.ai/?utm_source=github&utm_medium=agent-video-skills&utm_campaign=repo-cta"><strong>Try Meltica →</strong></a>
  &nbsp;·&nbsp; <a href="MELTICA.md">Read the product story</a>
  &nbsp;·&nbsp; <a href="#skills">Copy the skills</a>
</p>

<p align="center">
  <a href="https://meltica.ai/?utm_source=github&utm_medium=agent-video-skills&utm_campaign=repo-links">Website</a>
  · <a href="https://meltica.ai/blog?utm_source=github&utm_medium=agent-video-skills&utm_campaign=repo-links">Blog</a>
  · <a href="https://x.com/Meltica_felo">X</a>
</p>

---

# Agent Video Skills

A curated collection of **Agent Skills (SKILL.md)** for AI video creation — from prompting and generation to editing, subtitles and programmatic motion graphics.

> **About Meltica** — This collection is brought to you by the team behind [Meltica](https://meltica.ai), an AI promo-video platform for product brands, App & SaaS teams and local businesses. Turn an idea or a reference video into a short-video plan you can review and publish. [Learn more →](MELTICA.md)

一个面向 AI 视频创作的 **Agent Skills（`SKILL.md`）** 精选集：覆盖从提示词、生成到剪辑、字幕与代码化动效的全链路。

> **License:** MIT. Every skill in this repo is an original, rewritten adaptation **inspired by** an upstream MIT-licensed project. Inspiration, author and source URL are credited in each skill's `SKILL.md` (see [Credits](#credits)). No upstream source files are copied verbatim.
>
> 本仓库为 MIT 协议。每个 skill 都是参考上游 MIT 项目后**独立改写**的版本，灵感来源、作者与源地址均在各自 `SKILL.md` 中标注。未逐字复制任何上游源文件。

## What is an Agent Skill?

An Agent Skill is a folder with a `SKILL.md` file that teaches a coding agent how to perform one kind of task. Compatible agents (Claude Code, Codex, Cursor, WorkBuddy and others following the open Agent Skills format) auto-discover these files from a skills directory and load them when a request matches the description.

## Install

Install the whole collection as a plugin marketplace:

```bash
# in Claude Code
/plugin marketplace add <owner>/agent-video-skills
/plugin install agent-video-skills
```

Or copy individual skills into your agent's skills directory:

```bash
# Claude Code — all projects
cp -r skills/<skill-name> ~/.claude/skills/

# Claude Code — one project
cp -r skills/<skill-name> .claude/skills/

# Codex
cp -r skills/<skill-name> .agents/skills/
```

> **Note:** the `owner` field in `.claude-plugin/marketplace.json` and the `<owner>` placeholder in the install command above are intentionally kept neutral. Fill them in only if the marketplace is published under a named account.

## Skills

23 skills across six stages of the video workflow. Each link opens the full SKILL.md.

### Plan & prompt

| Skill | What it does | Use it when… |
| --- | --- | --- |
| [`video-prompt-studio`](skills/video-prompt-studio) | Turns an idea into a structured JSON video prompt — scene, characters, camera, dialogue, audio — with optional reference-image binding | you have a rough idea and need a model-ready prompt before generating |
| [`video-understanding`](skills/video-understanding) | Builds a scene-level index of a video: cut points, ASR transcript, per-scene visual observations, silence windows, a fused timeline and a writing brief | you need to recap, summarize or index a long video from real facts |
| [`ugc-ad-scripts`](skills/ugc-ad-scripts) | Writes phone-filmable UGC ad scripts with hook, body, CTA, 3–5 hook variants, delivery notes and disclosure lines | you need a creator-style vertical ad script that is ready to film |
| [`product-video-hooks`](skills/product-video-hooks) | Writes product-video openings as three agreeing layers — first frame, spoken line and text overlay — matched to buyer awareness and claim rules | you need the first 2–3 seconds of a TikTok, Reels or Meta product video |

### Generate

| Skill | What it does | Use it when… |
| --- | --- | --- |
| [`openrouter-video-gen`](skills/openrouter-video-gen) | Generates short clips via an async video API — cheapest suitable model first, one clip at a time, cost reported after each | you want a quick meme, promo or social clip from a prompt or a start image |
| [`seedance-video`](skills/seedance-video) | Plans multi-shot videos, writes Seedance prompts, quotes credits, renders cheap drafts and chains shots from the previous last frame | you want a multi-shot story, ad or explainer with staged approval before spend |
| [`text-to-video`](skills/text-to-video) | Conversational text-to-video with a draft → edit → export loop over a hosted backend | you want to refine a video through follow-up messages instead of one-shot generation |

### Avatars & lip sync

| Skill | What it does | Use it when… |
| --- | --- | --- |
| [`ai-avatar`](skills/ai-avatar) | Trains a consented digital twin or photo avatar and speaks lines in a cloned voice, judged mouth-to-mouth against real footage | the person on screen should be a specific person saying words they never recorded |
| [`lipsync`](skills/lipsync) | Drives a face's mouth from an audio track — portrait + audio, video + audio, or generate-and-sync from a script | you need to sync lips to a voice or dub a line onto existing footage |

### Programmatic video

| Skill | What it does | Use it when… |
| --- | --- | --- |
| [`motion-graphics-video`](skills/motion-graphics-video) | Directs then renders a motion-graphics MP4 from HTML/CSS/SVG with Chromium and ffmpeg, with optional synthesized effects | you want a directed explainer, launch film or kinetic-typography piece with no live action |
| [`remotion-video`](skills/remotion-video) | Builds a product or brand video in React + Remotion, from an approved brief and storyboard to a rendered MP4 | you want a repeatable, code-built promo or product demo |
| [`remotion-best-practices`](skills/remotion-best-practices) | Routes to the precise Remotion rule for animation, timing, captions, audio, charts, 3D and more | you are writing or debugging Remotion code and need the correct API pattern |

### End-to-end production

| Skill | What it does | Use it when… |
| --- | --- | --- |
| [`ai-video-production`](skills/ai-video-production) | Full narrated-explainer and music-video pipeline: script, storyboard with decision log, TTS + ASR check, VO-driven timing, Remotion graphics, publish | a solo creator is producing a finished explainer, tutorial or music video |

### Edit, captions & delivery

| Skill | What it does | Use it when… |
| --- | --- | --- |
| [`ffmpeg-video-edit`](skills/ffmpeg-video-edit) | 40+ local FFmpeg tools with a machine-readable contract and verified output: cut, join, reframe, speed, captions, loudness, HDR→SDR, exports | you need reliable, local, verifiable editing without an API key |
| [`ai-video-editor`](skills/ai-video-editor) | Natural-language ffmpeg + yt-dlp editing: trim, merge, silence, shorts, subtitles and YouTube clips | you want quick command-level edits, including from a YouTube URL |
| [`video-subtitle`](skills/video-subtitle) | Extracts, transcribes, translates, burns and visually edits subtitles using Whisper + ffmpeg, including bilingual output | you need to add, translate or burn subtitles, or review them in a visual editor |
| [`video-localization`](skills/video-localization) | Ships one approved master in many languages: dubbing, per-market captions and translated text baked into images, all from the master | you are localizing a video or ad into multiple markets |
| [`watch-video`](skills/watch-video) | Downloads a video, extracts timestamped frames and a transcript, then reads both so the agent can answer about its contents | you share a video/reel URL and ask what is in it, what was said, or to find a moment |
| [`thumbnail-video`](skills/thumbnail-video) | Generates distinct 1280×720 thumbnail variants from video frames with HTML/CSS-rendered caption text for A/B testing | you need YouTube thumbnails or a video cover with readable title text |
| [`video-enhance`](skills/video-enhance) | Repairs and finishing-passes existing footage — upscale, denoise, deblur, stabilize, interpolate, restore — with model choice by problem and async API lifecycle | a clip is soft, noisy, low-res or flickery and needs enhancement before delivery |
| [`video-to-shorts`](skills/video-to-shorts) | Turns a podcast, interview, talk or stream into vertical shorts: timestamped transcript, candidate scoring, new hook, captions and 1080×1920 delivery | you want to repurpose one long video into self-contained shorts for TikTok, Reels or Shorts |
| [`video-clip-extractor`](skills/video-clip-extractor) | Finds highlight moments in long videos or livestreams and packages them with titles, covers, subtitles and source timestamps | you want shareable highlight clips from a Bilibili/YouTube URL or a local recording |
| [`sound-design`](skills/sound-design) | Reads a script or edit moment by moment, chooses fitting sound layers, then generates WAV/48 kHz assets via API or local synthesis | you need music, SFX, transitions, ambience or UI sounds planned and produced for specific moments |

## Credits

All upstream projects are MIT-licensed. Full license texts and copyright notices are preserved in each source repository; this project credits them as the inspiration for independently rewritten skills.

| Skill | Source project | Author | License |
| --- | --- | --- | --- |
| video-prompt-studio | [Citrus-bit/Anaxa — video-generation](https://github.com/Citrus-bit/Anaxa/tree/HEAD/skills/public/video-generation) | Bytedance / DeerFlow / MedrixFlow Authors | MIT |
| video-understanding | [zenstory-ai/video-recap-skills — video-understanding](https://github.com/zenstory-ai/video-recap-skills/tree/HEAD/skills/video-understanding) | PiteChen | MIT |
| openrouter-video-gen | [alextitonis/fly.ai — video-gen](https://github.com/alextitonis/fly.ai/tree/main/.claude/skills/video-gen) | alextitonis | MIT |
| seedance-video | [AiuniVid/seedance-video-skill](https://github.com/AiuniVid/seedance-video-skill) | AiuniVid | MIT |
| text-to-video | [LeoYeAI/agent-master-skills — text-to-video-generator](https://github.com/LeoYeAI/agent-master-skills) | LeoYeAI | MIT |
| motion-graphics-video | [farhan-syah/motion-video-skill](https://github.com/farhan-syah/motion-video-skill) | farhan-syah | MIT |
| remotion-video | [LeoYeAI/agent-master-skills — remotion-video-generator](https://github.com/LeoYeAI/agent-master-skills) | LeoYeAI | MIT |
| remotion-best-practices | [Karanjot786/agent-skills-cli — remotion-best-practices](https://github.com/Karanjot786/agent-skills-cli) | Karanjot786 | MIT |
| ai-video-production | [Catnip202X/ai-video-production](https://github.com/Catnip202X/ai-video-production) | Catnip202X | MIT |
| ffmpeg-video-edit | [kajisho5/ffmpeg-skill](https://github.com/kajisho5/ffmpeg-skill) | kajisho5 | MIT |
| video-subtitle | [Crazy-MT/video-subtitle](https://github.com/Crazy-MT/video-subtitle) | Crazy-MT | MIT |
| ai-video-editor | [shahafg1/ai-video-editor](https://github.com/shahafg1/ai-video-editor) | shahafg1 | MIT |
| ai-avatar | [MengTo/Skills — create-ai-avatar](https://github.com/MengTo/Skills/tree/main/agent-skills/media/create-ai-avatar) | Meng To | MIT |
| lipsync | [genmedia-labs/skills — lipsync](https://github.com/genmedia-labs/skills/tree/main/lipsync) + [layerai/skills — layer-talking-characters](https://github.com/layerai/skills) | genmedia-labs / Layer AI | MIT |
| video-localization | [layerai/skills — layer-localization](https://github.com/layerai/skills/tree/main/plugins/layer/skills/layer-localization) + [elevenlabs/skills — dubbing](https://github.com/elevenlabs/skills/tree/main/dubbing) | Layer AI / ElevenLabs | MIT |
| watch-video | [ryankolean/summit-claude-skills — watch-video](https://github.com/ryankolean/summit-claude-skills/tree/main/skills/watch-video) | Summit Software Solutions LLC | MIT |
| thumbnail-video | [smitmartijn/claude-skills — thumbnail-video](https://github.com/smitmartijn/claude-skills/tree/HEAD/thumbnail-video) | Martijn Smit | MIT |
| video-enhance | [calesthio/generative-media-skills — topaz-video-enhancement](https://github.com/calesthio/generative-media-skills/tree/main/skills/providers/video-enhancement/topaz-video-enhancement) | generative-media-skills contributors | MIT |
| video-to-shorts | [social-media-skills — video-to-shorts-skill](https://github.com/social-media-skills/video-to-shorts-skill), [Jakeschincariol/youtube-agent-skill — yt-shorts](https://github.com/Jakeschincariol/youtube-agent-skill/tree/main/skills/yt-shorts), [Melvynx/video-agent-skills — clips](https://github.com/Melvynx/video-agent-skills/tree/main/skills/clips) | social-media-skills / Jakeschincariol / Melvynx | MIT |
| sound-design | [dodoxtech/sonic-skill — sound-generation](https://github.com/dodoxtech/sonic-skill/tree/main/skills/sound-generation) | dodoxtech | MIT |
| video-clip-extractor | [linzzzzzz/openclip — video-clip-extractor](https://github.com/linzzzzzz/openclip/tree/main/.claude/skills/video-clip-extractor) | OpenClip Contributors | MIT |
| ugc-ad-scripts | [mbfinotti/advertising-skills — ugc-ad-scripts](https://github.com/mbfinotti/advertising-skills/tree/HEAD/skills/ugc-ad-scripts) | Nativa Labs | MIT |
| product-video-hooks | [vargHQ/skills — product-video-hooks](https://github.com/vargHQ/skills/tree/main/product-video-hooks) | vargai Inc. | MIT |

See each skill's `SKILL.md` → **Inspiration & credit** section for details.

## Disclaimer

These skills are instruction sets for coding agents, not turnkey video renderers. Many call third-party APIs or require local tools (FFmpeg, Python, Node). Check each skill's prerequisites, and review third-party skill source before installing. Costs incurred through third-party APIs are the user's responsibility; skills that spend credits must quote and ask for approval first.
