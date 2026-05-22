# Bramwell App

> Bramwell — your AI butler for the smart home. Alfred runs real devices, drives the open internet on your behalf, and keeps quiet excellence across every household errand.

## Installation

1. Add the Bramwell repository: **Settings → Apps → App Store → ⋮ → Repositories → `https://github.com/bengulliford/bramwell-addons`**.
2. Open the Bramwell app from the store and click **Install** (Supervisor pulls the pre-built image — no on-device build).
3. (Optional) On the **Configuration** tab set `frigate_base_url` — the URL of your Frigate instance (e.g. `http://192.168.1.50:5000`). The credential-encryption key is auto-generated on first start and persisted to `/data` — there's nothing to configure.
4. **Start** the app. The first start pre-creates state under `/data` and may take ~60 s.
5. Click **Open Web UI** (uses HA Ingress — no port mapping required).
6. Enter your **license key** and **LLM provider** from the Bramwell **Settings** page after first launch — these are not app options (Brain reads them from its own settings store, not env vars).

## Configuration reference

| Option | Required | Default | Description |
| --- | --- | --- | --- |
| `ha_url` | yes | `http://supervisor/core` | HA REST/WS base URL. The default proxies through the Supervisor; only override if you know what you're doing. |
| `frigate_base_url` | no | — | Frigate base URL for the Alfred camera-context feature. |

> The credential-encryption key is **auto-generated** on first start and stored at `/data/.encryption_secret` (survives upgrades). There is no option for it.

> The license key and LLM provider/token are **not** app options — set them in the Bramwell Settings UI after first launch. Brain reads them from its settings store, so values pasted into app options would be ignored.

## Logs

The app log surfaces Brain's `Microsoft.Extensions.Logging` output with the bashio header prefix. Use **Settings → Apps → Bramwell → Log** to read live; download for support reports.

## Support

See [`docs/SUPPORT.md`](https://github.com/bengulliford/HomeClaw/blob/dev/docs/SUPPORT.md) for the redacted bundle workflow and where to file reports.
