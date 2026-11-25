---
name: video-subtitle
description: >-
  Add, generate, translate or burn subtitles into a video. Use when the user wants hardcoded or
  burned-in subtitles, speech-to-SRT transcription, translation of existing subtitles, dual-language
  subtitles (original + translation), or visual subtitle editing. Triggers: "add subtitles",
  "transcribe this video", "translate subtitles", "burn subtitles", "generate SRT", "双语字幕",
  "给视频加字幕", "烧录字幕".
license: MIT
---

# Video subtitle pipeline

Full workflow: **extract audio → speech-to-text → translate → burn subtitles**.

## Prerequisites

- `ffmpeg` and `ffprobe` on `PATH` — verify with `ffmpeg -version`.
- Python 3 with `openai-whisper` — `pip install openai-whisper`.
- First transcription downloads a Whisper model (~140 MB for `base`); models cache in
  `~/.cache/whisper/`.
- macOS / Linux / Windows. A local-only flow — nothing is uploaded.

Scripts referenced below belong to the installed skill (`<skill-dir>/scripts/`) and are not bundled
with this repository.

## Workflow

### Step 1 — Extract audio

```bash
python3 <skill-dir>/scripts/extract_audio.py "<video>" --output "<audio>.wav"
```

Output is 16 kHz mono WAV — best for Whisper accuracy. Omit `--output` for a default name.

### Step 2 — Transcribe with Whisper

```bash
python3 <skill-dir>/scripts/transcribe.py "<audio>.wav" --model base --output "<name>.srt"
```

Models: `tiny` (fastest) · `base` (good default) · `small` · `medium` · `large` (best accuracy).
The script prints the detected language — use it to decide whether translation is needed.

### Step 3 — Translate

If the detected language differs from the target, translate the SRT in place:

1. Read the generated SRT to get all segments with timestamps.
2. Translate each segment's text, preserving structure exactly — index and timestamps unchanged.
3. Write the result to `<name>.<target-lang>.srt`.

**After translating, open the visual editor** so the user can review and tweak without an extra step:

```bash
python3 <skill-dir>/scripts/serve_preview.py "<video>" "<translated>.srt"
# SRT-only mode (no video handy)
python3 <skill-dir>/scripts/serve_preview.py "<translated>.srt"
```

The editor runs entirely on a local server (default `http://127.0.0.1:5173/`): left is a video
player with a live subtitle overlay; right is a list of segments to edit, seek to, delete or add.
**Save SRT** downloads the corrected file; **Export video** burns the subtitles using a Pillow /
moviepy path that works even on ffmpeg builds without libass.

### Step 4 — Burn subtitles

Single-language mode:

```bash
python3 <skill-dir>/scripts/burn_subtitle.py "<video>" "<srt>" \
  --output "<out>.mp4" --style default
```

Style presets: `default`, `streaming` (Netflix-like), `white_shadow` (cinematic),
`yellow_black` (high contrast), `minimal`. Custom styles:

```bash
--custom "FontSize=20,PrimaryColour=&H00FFFFFF,OutlineColour=&H00000000"
```

Dual-language mode (original + translation):

```bash
python3 <skill-dir>/scripts/burn_dual_subtitle.py "<video>" "<orig>.srt" "<translated>.srt" \
  --output "<out>.mp4"
```

## Full example

User: "帮我把 lecture.mp4 生成中英双语字幕"

1. `extract_audio.py lecture.mp4` → `lecture.wav`
2. `transcribe.py lecture.wav --model base` → `lecture.srt` (prints `Detected language: zh`)
3. Translate → `lecture.english.srt` → open editor for review
4. `burn_dual_subtitle.py lecture.mp4 lecture.srt lecture.english.srt` → `lecture.dual.mp4`

## Platform notes

- **Linux:** install `fonts-noto-cjk` (Debian/Ubuntu) or `noto-fonts-cjk` (Arch); pass
  `--custom "FontName=Noto Sans CJK SC,..."`.
- **Windows:** prefer `Microsoft YaHei` or `SimHei` via `--custom "FontName=Microsoft YaHei,..."`.
- **macOS:** `PingFang SC` and `Helvetica` are available.
- **Sandboxed paths:** write intermediates to `/tmp/` first, then copy the final output back.

## Troubleshooting

| Problem | Fix |
|---------|-----|
| `ffmpeg: command not found` | Install ffmpeg and add it to `PATH` |
| `ModuleNotFoundError: whisper` | `pip install openai-whisper` |
| Subtitles invisible | ffmpeg `subtitles=` needs an absolute SRT path with no special characters |
| No libass in ffmpeg | Use `burn_moviepy.py` or `serve_preview.py` instead of the `subtitles` filter |
| Chinese renders as boxes | Install a CJK font; set `FontName` explicitly |

## Inspiration & credit

This skill is an original, rewritten adaptation **inspired by** `video-subtitle` from
Crazy-MT/video-subtitle. Its scripts and editor are external tools and are not bundled here.

- Source: https://github.com/Crazy-MT/video-subtitle
- License: MIT, Crazy-MT.
- No upstream source files are copied verbatim.
