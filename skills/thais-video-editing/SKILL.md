---
name: thais-video-editing
description: Route Claude video-editing work across this project's three skills. Use when the user wants to edit video with Claude, tighten a recording, make shorts/clips, file memes/screenshots/sounds, or asks for cut-video, clipify, or the assets bot.
---

# Thais video editing

This repo is one video-editing toolkit with three skills. Pick the matching skill and follow **that** skill's `SKILL.md` — do not improvise a fourth pipeline.

| User intent | Skill | Path |
| --- | --- | --- |
| Tighten a long take: remove silences, ums, fillers, retakes; keep laughs | **cut-video** | `skills/cut-video/SKILL.md` |
| Long video → social shorts: find moments, 9:16 reframe, opus captions | **clipify** | `skills/clipify/SKILL.md` |
| Save a dropped file, YouTube link, or image URL into `~/assets` | **assets-bot** | `skills/slack-assets-bot/SKILL.md` |

## Typical order

1. **File taste** — assets-bot (memes, screenshots, sounds, reference clips)
2. **Tighten the long recording** — cut-video
3. **Cut social clips from the cleaned long video** — clipify

If the user only asks for one of those, run only that skill.

## How to run

- Skill dirs in this repo: `skills/<name>/`. Scripts live next to each `SKILL.md` (clipify `scripts/`, cut-video `make_review.py`, assets-bot `bot.py` / `setup.py`).
- Read the chosen `SKILL.md` fully before acting. Use its working directories (`/tmp/cut-video/`, `/tmp/clipify/`, `~/assets`).
- cut-video and clipify are local (ffmpeg + whisper, Apple Silicon VideoToolbox). assets-bot skill mode files from chat; the Slack bot is optional (`skills/slack-assets-bot/INSTALL.md`).

## Do not

- Mix cut-video silence heuristics into clipify, or skip MFA/ground-truth steps in cut-video
- Overwrite files in the asset library
- Commit `.env` or Slack tokens
