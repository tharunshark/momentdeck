# MomentDeck

MomentDeck is a local-first website for turning a stream or video link into short highlight candidates. Paste a link you are authorized to use, review the suggested clips, then download and post them yourself.

## What it does

- Accepts supported Twitch, YouTube, and Kick video links, plus live channel links where supported by the source pipeline.
- Requires an explicit rights confirmation before link lookup or processing. The confirmation is recorded, but the app cannot independently verify permission.
- Suggests moments using the adapted project's speech, audio, and optional AI selection pipeline.
- Shows the clip's source start time, duration, and selection score so you can inspect the moment before downloading it.
- Keeps publishing manual. There is no automatic or one-click upload to social platforms.

## What it does not do yet

- It does not connect to Twitch EventSub or YouTube Live Chat APIs and does not analyze chat velocity or emotes.
- It does not guarantee 4K. The adapted pipeline targets up to 1080p source and 1080×1920 vertical clips.
- It does not use official Twitch or YouTube APIs to retrieve video. The inherited source pipeline uses `yt-dlp`; use only content you own or have permission to process and follow applicable platform rules.
- It is a local prototype, not a public multi-user service. The default server binds to `127.0.0.1` and accounts are off by default.

## Run locally

You need Python 3.13, FFmpeg, and FFprobe. From this directory:

```sh
python3.13 -m venv .venv
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python -m studio.server
```

Open [http://127.0.0.1:8765](http://127.0.0.1:8765). The speech model downloads on first use. AI-assisted selection is optional; configure a provider in Settings or use the available audio-based fallback.

## Project origin and license

MomentDeck is an adapted fork of [PeakCut](https://github.com/haziqahmedqasmi/peakcut). It reuses the upstream clip-processing foundation under the MIT License; see [`LICENSE`](LICENSE) for the required upstream notice. MomentDeck's name, workflow changes, permission gate, manual-review focus, and source-time review details are this project's adaptations. It is not a claim of authorship over PeakCut's underlying code.

## Before hosting publicly

This prototype is intended for one person on their own computer. A hosted version needs a review of authentication, storage isolation, retention/deletion, source rights, provider API compliance, and deployment security. Official provider integrations and chat-signal detection remain future work.
