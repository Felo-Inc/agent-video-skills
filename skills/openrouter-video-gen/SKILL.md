---
name: openrouter-video-gen
description: >-
  Generate short AI video clips (memes, promos, social posts) from a text prompt or a start image
  through the OpenRouter video API. Use when someone asks to make, generate or render a video,
  clip, short, reel or animated meme. Picks the cheapest suitable model first, generates one clip
  at a time, and reports the cost after each clip.
---

# Video generation (OpenRouter)

Generate a short clip with OpenRouter's async video API: submit a job, poll it, download the MP4.
The entire flow runs through one Python script that uses only the standard library.

## Setup (once per machine)

- An OpenRouter key in the environment: `OPENROUTER_API_KEY=sk-or-...`, with a **spend cap** set
  in the OpenRouter dashboard. Video costs escalate quickly.
- Python 3.9+. No packages to install.

## Rules for the agent

1. **Cost first.** Before the first clip, run `list` and pick the cheapest model that fits.
   Default to a cheap 480p "lite" tier, about 4–6 seconds. Move to premium models (Veo, Kling,
   etc.) only when the user asks for quality.
2. **One clip at a time.** Make one clip, show the file and its cost (`usage.cost`), then ask
   before making more. Never start a batch without the user agreeing to a total ("5 clips ≈
   $0.50, OK?").
3. **Short and vertical by default.** For social posts use `--aspect 9:16 --duration 5`. Ask only
   when a different shape genuinely matters.
4. **Prompt like a shot list:** subject, action, camera, style, lighting, mood — one scene per clip.
5. **No real people's likeness, no brand logos or trademarks** unless the user owns them. No
   sexual, violent or deceptive content.
6. **Outputs** go in `./videos/` (or where the user says), with a `.json` sidecar holding the
   prompt, model and cost. Never print or share the signed `urls` from the API — anyone holding
   one can download the clip.
7. On failure, show the `error` and change the prompt or model. Do not loop retries.

## Commands

Adapt the script path to where this skill is installed.

```bash
# list video models (look for "lite", 480p, low per-second price)
python <skill-dir>/gen_video.py list

# text -> video
python <skill-dir>/gen_video.py gen --model <model-id> \
  --prompt "cartoon fly surfing a wave of coffee, slow motion, sunny" \
  --duration 5 --aspect 9:16 --resolution 480p

# image -> video (animate a still, used as first frame)
python <skill-dir>/gen_video.py gen --model <model-id> \
  --prompt "the fly blinks and takes off" --image ./fly.png

# no audio (cheaper on some models)
python <skill-dir>/gen_video.py gen ... --no-audio
```

The script prints the job id while polling, then the saved path and cost. If interrupted, resume
with `python gen_video.py fetch <job-id>`.

## Exposing the script as an agent tool

A minimal tool definition:

```json
{
  "name": "generate_video",
  "description": "Generate one short video clip. Returns file path and cost. Call once per clip; confirm with the user before generating more.",
  "input_schema": {
    "type": "object",
    "properties": {
      "prompt": { "type": "string" },
      "model": { "type": "string", "description": "OpenRouter video model id; cheapest suitable" },
      "duration": { "type": "integer", "default": 5 },
      "aspect_ratio": { "type": "string", "default": "9:16" },
      "resolution": { "type": "string", "default": "480p" },
      "image_path": { "type": "string", "description": "optional first-frame image" }
    },
    "required": ["prompt", "model"]
  }
}
```

The handler runs `gen_video.py gen ...` and returns its last line (JSON). Give sub-agents this
same skill and the same rules: one clip, report cost, wait for approval.

## Notes

- A job takes 30 seconds to a few minutes. The script polls every 15 s and gives up after 15 min.
- To join clips or add captions, use ffmpeg: `ffmpeg -f concat -safe 0 -i list.txt -c copy out.mp4`.
- Each run is a new billed job — only tweak the prompt after watching the previous clip.

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** the `video-gen` skill in
alextitonis/fly.ai.

- Source: https://github.com/alextitonis/fly.ai/tree/main/.claude/skills/video-gen
- License: MIT, alextitonis.
- No upstream source files are copied verbatim. `gen_video.py` is referenced as an external
  tool and is not bundled here.
