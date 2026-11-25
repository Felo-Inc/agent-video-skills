# Agent Video Skills

A curated collection of **Agent Skills (SKILL.md)** for AI video creation — from prompting and generation to editing, subtitles and programmatic motion graphics.

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

| Skill | What it does | Inspired by |
| --- | --- | --- |
| [`video-prompt-studio`](skills/video-prompt-studio) | Turn an idea into a structured, model-ready JSON video prompt with reference-image guidance | Citrus-bit/Anaxa (video-generation) |
| [`openrouter-video-gen`](skills/openrouter-video-gen) | Generate short clips via OpenRouter's async video API — cost-first, one clip at a time | alextitonis/fly.ai (video-gen) |
| [`seedance-video`](skills/seedance-video) | Plan multi-shot Seedance videos, write prompts, quote and render by last-frame chaining | AiuniVid/seedance-video-skill |
| [`text-to-video`](skills/text-to-video) | Conversational text-to-video with draft → edit → export loop | LeoYeAI/agent-master-skills |
| [`motion-graphics-video`](skills/motion-graphics-video) | Direct and render a motion-graphics MP4 from HTML/CSS/SVG with Chromium + ffmpeg | farhan-syah/motion-video-skill |
| [`remotion-video`](skills/remotion-video) | Build a product/brand video in React + Remotion, from brief to rendered MP4 | LeoYeAI + TechNomadCode |
| [`remotion-best-practices`](skills/remotion-best-practices) | Domain-rule router for Remotion: animation, captions, audio, charts, 3D and more | Karanjot786/agent-skills-cli |
| [`ai-video-production`](skills/ai-video-production) | End-to-end narrated explainer / music-video production for a solo creator | Catnip202X/ai-video-production |
| [`ffmpeg-video-edit`](skills/ffmpeg-video-edit) | 40+ local FFmpeg editing tools with a machine-readable contract and verification | kajisho5/ffmpeg-skill |
| [`video-subtitle`](skills/video-subtitle) | Extract, transcribe, translate, burn and visually edit subtitles (Whisper + ffmpeg) | Crazy-MT/video-subtitle |
| [`ai-video-editor`](skills/ai-video-editor) | Natural-language ffmpeg + yt-dlp editing: trim, merge, silence, shorts, YouTube clips | shahafg1/ai-video-editor |

## Credits

All upstream projects are MIT-licensed. Full license texts and copyright notices are preserved in each source repository; this project credits them as the inspiration for independently rewritten skills.

| Skill | Source project | Author | License |
| --- | --- | --- | --- |
| video-prompt-studio | [Citrus-bit/Anaxa — video-generation](https://github.com/Citrus-bit/Anaxa/tree/HEAD/skills/public/video-generation) | Bytedance / DeerFlow / MedrixFlow Authors | MIT |
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

See each skill's `SKILL.md` → **Inspiration & credit** section for details.

## Disclaimer

These skills are instruction sets for coding agents, not turnkey video renderers. Many call third-party APIs or require local tools (FFmpeg, Python, Node). Check each skill's prerequisites, and review third-party skill source before installing. Costs incurred through third-party APIs are the user's responsibility; skills that spend credits must quote and ask for approval first.
