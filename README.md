# Bramwell — Home Assistant Apps

Your AI butler for the smart home. Alfred runs real devices, drives the open internet on your behalf, and keeps quiet excellence across every household errand.

## Install

[![Add repository to your Home Assistant.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fbengulliford%2FBramwell)

1. Click the button above — or **Settings → Apps → App Store → ⋮ → Repositories** and add:
   `https://github.com/bengulliford/Bramwell`
2. Find **Bramwell** or **Bramwell Pro** in the store and click **Install** (pulls a pre-built image — no on-device build).
3. **Start** it, then **Open Web UI**. Enter your license + LLM provider in Bramwell Settings.

## Apps in this repository

- **Bramwell** — the AI-butler Brain + dashboard; the free app, and the place to start. See [`bramwell/DOCS.md`](bramwell/DOCS.md).
- **Bramwell Pro** — the same Brain + dashboard with the browser-agent (Chromium/Playwright) bundled on-box, so Alfred can run web errands on your own hardware. Requires a **Local Pro** license ([bramwell.app](https://bramwell.app)). See [`bramwell-pro/DOCS.md`](bramwell-pro/DOCS.md).

The two apps share settings, license, and credentials (`/config/.bramwell/`), so you can switch between them without losing data — just don't run both at once.
