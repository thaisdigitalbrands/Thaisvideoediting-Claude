# Thaisvideoediting Claude

One Claude video-editing project with three skills. Point them at **your** video files — there are no bundled sample clips.

1. **cut-video** — tighten long recordings (silences, ums, retakes; keep laughs)
2. **clipify** — turn a long video into social-ready shorts (9:16, face-pan, captions)
3. **assets-bot** — file dropped images, clips, sounds, and YouTube links into a local library

Typical flow: save assets → tighten the long take → cut shorts from the cleaned video.

Third-party MIT-licensed skills; each folder keeps its original LICENSE. See [NOTICE.md](NOTICE.md).

## Layout

```
skills/
  thais-video-editing/   # router: which skill to use
  cut-video/             # tighten long recordings
  clipify/               # social shorts from a long video
  slack-assets-bot/      # file dropped assets into a local library
.cursor/skills/          # Cursor project skills (symlinks)
.claude/skills/          # Claude Code project skills (symlinks)
.claude-plugin/          # Claude Code plugin manifest
```

Open this folder in **Cursor** and the three skills load from `.cursor/skills/`.

## Install for Claude Code (slash commands)

```bash
cd "/Users/thaisbretz/Claude things/Thaisvideoediting-Claude"
mkdir -p ~/.claude/skills
for s in cut-video clipify slack-assets-bot thais-video-editing; do
  ln -sfn "$(pwd)/skills/$s" ~/.claude/skills/$s
done
```

Restart Claude Code. Then `/cut-video`, `/clipify`, and `/assets-bot` are available.

## Requirements

Shared (cut-video + clipify):

- macOS (VideoToolbox). Drop `-hwaccel videotoolbox` on Linux/Windows.
- `ffmpeg` with libx264 — `brew install ffmpeg`
- Whisper — `pip install openai-whisper`

clipify also needs `numpy`. cut-video auto-installs Montreal Forced Aligner on first run.

assets-bot (Slack app, optional): Python 3.10+, `yt-dlp`, Slack tokens. Skill mode needs no Slack app — see `skills/slack-assets-bot/INSTALL.md`. Copy `skills/slack-assets-bot/.env.example` to `.env` locally; never commit `.env`.

## Usage

Paste a path to **your** recording (or drop a file). Working copies land in `/tmp/cut-video/` and `/tmp/clipify/`; finished files go next to the source (`cut_out/`, `clipify_out/`).

| You want | Skill | Trigger |
| --- | --- | --- |
| Shorter long-form, same jokes | cut-video | “cut this”, “tighten this”, “remove silences” |
| TikTok / Reels / Shorts from a long video | clipify | “clipify”, “make shorts”, “vertical clips” |
| Save a meme, screenshot, sound, or YouTube URL | assets-bot | drop a file, “save this”, `name:`, `project:` |

Details: `skills/cut-video/README.md`, `skills/clipify/README.md`, `skills/slack-assets-bot/README.md`.

Do not push this combined project to the `upstream-*` remotes.
