# Bramwell Pro App

> Bramwell Pro — Alfred plus the on-box browser-agent. Runs real devices, drives the open internet on your behalf, and handles household errands, all on your own hardware (Local Pro).

The fat variant of the [Bramwell](../bramwell/) app: the same Brain + dashboard, plus the browser-agent (Chromium + Playwright) bundled into the same image as a second service, so Alfred can carry out web errands on your own hardware — nothing else to install or wire up.

Bramwell Pro requires a **Local Pro** license key, activated in Bramwell **Settings** after first launch — see [bramwell.app](https://bramwell.app).

- Install + configuration: [`DOCS.md`](DOCS.md)
- Release history: [`CHANGELOG.md`](CHANGELOG.md)
- Manifest: [`config.yaml`](config.yaml) — mirrored from the source repo's `addon/config.pro.yaml`; Supervisor pulls the pre-built `ghcr.io/bengulliford/bramwell-pro-{arch}` image.

Settings, license, and stored credentials are shared with the lean Bramwell app via `/config/.bramwell/`, so you can switch between the two without losing data — but don't run both at the same time.
