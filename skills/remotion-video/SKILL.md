---
name: remotion-video
description: >-
  Make a short product or brand video (promo, launch, explainer, demo or social clip) entirely in
  React + Remotion, from an approved brief and storyboard to a rendered MP4 with sound. Use when the
  user wants a programmatic, code-built video with precise timing, branded scenes and repeatable
  renders. Not for editing existing footage or simple slideshows.
---

# Remotion video

Build the video in code. The owner approves the idea and a storyboard before anything is built.

**CRITICAL Remotion v4 rules**

1. Use `.tsx` (not `.ts`) for files containing JSX.
2. Register compositions with `registerRoot` + `Composition`.
3. Always pass `fps` to `spring()`: `spring({ frame, fps, from: 0.8, to: 1 })`.
4. Get fps from `useVideoConfig()`: `const { fps } = useVideoConfig()`.
5. Render by composition name: `npx remotion render MyVideo out/video.mp4`.

## Workflow

1. **Brief.** Confirm the goal, audience, length, aspect ratio and call to action. If a product or
   company is featured, collect its brand data first — colors, logo, tagline, screenshots — by
   fetching the public website. Do not invent a brand palette.
2. **Storyboard.** Break the video into scenes with durations, on-screen copy and transitions.
   Present it and wait for approval before writing components.
3. **Scaffold.**

   ```bash
   npx --yes create-video@latest my-video --template blank
   cd my-video && npm install lucide-react
   ```

   Fix `package.json` scripts to use Remotion directly (replace any `bun` references):

   ```json
   { "scripts": { "dev": "npx remotion studio", "build": "npx remotion bundle" } }
   ```

4. **Build scenes.** One component per scene. Establish a persistent animated background layer
   outside scenes, then vary pacing (2–3 s punchy, 4–5 s dramatic). Open with a high-impact hook,
   carry the content in the middle, and close with an intentional, resolved ending. Use an icon
   library such as `lucide-react` — no hand-rolled SVG icons.
5. **Assets.** Put user assets, generated media and scraped brand assets under `public/`. Define
   durations in the composition and vary them deliberately.
6. **Preview.** Start Remotion Studio in the background and give the user a preview URL (a local
   port or a tunnel). The user reviews live; edits hot-reload.
7. **Render — only when the user explicitly asks to export.**

   ```bash
   npx remotion render CompositionName out/video.mp4
   ```

## File structure

```
my-video/
├── src/
│   ├── index.ts          # entry point
│   ├── Root.tsx          # registerRoot + Composition definitions
│   ├── index.css         # global styles
│   ├── MyVideo.tsx       # main component
│   └── scenes/           # scene components
├── public/
│   ├── images/brand/     # scraped brand assets
│   └── audio/            # background music
├── remotion.config.ts
└── package.json
```

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| `Expected ">" but found "schema"` | Use `.tsx` for JSX, not `.ts` |
| `useCurrentFrame() outside component` | Call hooks only inside a component |
| Spring looks linear | Pass `fps` and use an easing/damping config |
| Missing fonts | Load Google or local fonts explicitly before measuring text |

For advanced domain rules — captions, audio timing, charts, 3D, transitions — use the companion
`remotion-best-practices` skill.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `remotion-video-generator` from
LeoYeAI/agent-master-skills and the `remotion-video` skill in
TechNomadCode/AI-Product-Development-Toolkit.

- Sources:
  - https://github.com/LeoYeAI/agent-master-skills/tree/HEAD/skills/remotion-video-generator
  - https://github.com/TechNomadCode/AI-Product-Development-Toolkit/tree/main/agent-skills/remotion-video
- License: MIT, LeoYeAI / TechNomadCode.
- No upstream source files are copied verbatim.

---

## About this collection

This skill is part of [Agent Video Skills](https://github.com/Felo-Inc/agent-video-skills), an open collection from the team behind [Meltica](https://meltica.ai) — an AI promo-video platform for products, apps and local businesses. If you would rather use a finished workflow than assemble skills yourself, see [meltica.ai](https://meltica.ai) · [blog](https://meltica.ai/blog).
