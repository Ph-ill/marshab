# MarsHab

A tiny offline social game for a Raspberry Pi Pico W captive portal.

This public repo intentionally contains only the browser client source:
- `index.html` — the single-file game client
- `gift.mjs` — pure gift/passport reducers used by the client

Project shape
- Fully offline in the browser
- No external libraries or CDN assets
- Designed for a very small flash budget on Pico W hardware
- Uses a mock in-browser server during development, then talks to the Pico endpoints on device

Current focus
- Isometric room rendering and movement
- Owner/guest flows
- Shop, build mode, wardrobe, mini-game, live presence
- Gift buying, delivery, and reconcile flow

Notes
- This repo is a src-only publish mirror.
- Development happens in a separate private/local workspace so support files, docs, and agent project files are not published here.
