# MomentDeck handoff

This note is for the next AI or developer continuing the project. Read this first, then read the project `README.md`, `AGENTS.md`, `NOTICE`, and `LICENSE`.

## Project and repository

- Public repository: https://github.com/tharunshark/momentdeck
- Local source: `/Users/tharun/Documents/Codex/2026-11-17/referenced-chatgpt-conversation-this-is-an/stream-clipper-site`
- Product: local-first web interface that accepts stream/video links, requires an explicit rights confirmation, creates reviewable candidates, and lets the user download/post manually.
- This is an adapted PeakCut fork under MIT. Preserve the upstream attribution; do not claim the inherited processing engine as original work.

## User's product constraints

- Monitor only streamers/accounts the user is authorized to monitor. The rights checkbox is an honor-system confirmation and does not independently prove authorization.
- Never publish automatically. Keep every candidate reviewable and require the user to download and post it themselves.
- Do not process anyone's content without authorization.
- The user wants a distinct MomentDeck visual identity, not a lightly renamed PeakCut interface.
- Reference visual palette: warm cream/sand, muted teal, ocean blue, deep navy. Glass effects should remain subtle enough to keep controls readable.

## Work completed

- Public GitHub repository created and populated with the project source, runtime files, docs, tests, fonts, and deployment files. The current palette, logo, Twitch OAuth/chat velocity implementation, UI, and docs are synced to `main`. Demo videos, local data, virtual environments, secrets, and caches were excluded.
- Root README describes current limitations and MIT attribution.
- Manual publishing is kept in the clip review/download flow. Server routes for `/api/posts` reject publishing.
- UI was restyled to the cream/teal/ocean/navy palette with translucent glass surfaces. Landing page was updated to match.
- Logo SVGs and email PNG were recolored to navy, teal, cream, and muted sand.
- App's dashboard repository link now points to this MomentDeck repository.
- Local Python 3.13 dependencies are installed in `.venv-py313`. A local preview was started on `http://127.0.0.1:8876` using temporary smoke data.

## Chat velocity implementation in progress

The prior code already had a partial Twitch chat-rate detector, but it connected as an anonymous `justinfan` user. Current Twitch developer docs require an authenticated user token with `chat:read` for IRC chat, so that old approach was not reliable.

The current source now adds:

- Twitch OAuth app configuration keys: `PEAKCUT_TWITCH_CLIENT_ID` and `PEAKCUT_TWITCH_CLIENT_SECRET`.
- Twitch connect/refresh flow storing a per-user Twitch chat account with the user's account data.
- Authenticated Twitch IRC (`irc.chat.twitch.tv:6697`) with Twitch tag capability; counts `PRIVMSG` and Twitch emote-tag occurrences.
- A short-window message-rate and emote-rate spike signal combined with audio activity, and UI cards showing rates, baselines, connection state, and trigger reasons.
- Settings → Chat signals UI with Twitch app callback instructions and Connect/Disconnect actions.
- README and landing-page notes updated to say Twitch chat velocity is supported after authorization, while YouTube live chat is not integrated.

The code has not been tested against a real Twitch app/account or a live channel yet. Twitch OAuth configuration, chat permission, token refresh, IRC reconnection, emote-tag parsing, and the UI need end-to-end review. Use only an account/channel for which the user has permission.

## Important limitations / next work

1. **Finish runtime setup.** The local machine has no FFmpeg/FFprobe. Homebrew refuses installation until the macOS Xcode license is reviewed/accepted. The app UI loads, but actual clipping stays disabled until FFmpeg is installed. Do not accept Apple's license on the user's behalf.
2. The `.venv-py313` dependencies are installed. Start normally with `./.venv-py313/bin/python -m studio.server`; by default the app serves on `127.0.0.1:8765` and downloads its speech model. The current preview used `PEAKCUT_FETCH_MODEL=0`, data at `work/runtime-data`, and port 8876.
3. Chat velocity is Twitch-only. YouTube Live Chat API integration remains future work and needs Google OAuth scope/consent and quota handling. Twitch EventSub migration is also future work; current code uses Twitch's official IRC interface.
4. Video-source retrieval still uses inherited `yt-dlp`, not official Twitch/YouTube video APIs. Output is capped at 1080p; it does not guarantee or create 4K.
5. Do not run the inherited test suite unless the user asks for tests/verification. The local UI and settings page were visually checked; Twitch authorization against a real app/account and clip rendering have not been verified.

## Suggested next-AI instruction

Continue MomentDeck from this handoff. Inspect the current local and GitHub source, review the Twitch OAuth/IRC behavior against official Twitch documentation, and finish any runtime setup after the user personally accepts the Xcode license. Keep the app permission-based and manual-post-only. Do not publish, deploy, or process any stream content without the user's authorization. Implement YouTube live-chat support as a separate, clearly labeled step rather than implying it already works. Preserve PeakCut MIT attribution.
