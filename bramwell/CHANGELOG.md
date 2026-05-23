# Bramwell Add-on Changelog

## 1.0.0-beta.7 (2026-05-23)

- **Reports tab** — browse saved Smart Home Analysis reports and generate new ones; report styling fixed (renders correctly offline in the sandboxed viewer).
- **"Log in with Home Assistant"** for the standalone-tab surface (OAuth; Bramwell never sees your HA password).
- **Manual floor plans** via Home-Assistant-areas drag-and-drop.
- **Voice** — spoken-friendly TTS replies + an opt-in "Speak responses" toggle; the dashboard mic now works in Firefox/Safari by routing through your own HA speech-to-text.
- **Notes** render Markdown (bold/italics/lists/tables/code) properly.
- Settings now save consistently; numerous reliability fixes (LLM config, HA reconnect/circuit-breaker, license activation grace).

## 1.0.0-beta.3 (2026-05-15)

- First add-on release. Backlog [#18](../docs/BACKLOG.md) closes the install gap for HA-OS users.
- Multi-arch base images (`amd64`, `aarch64`).
- HA Ingress UI; Bramwell auth gate trusts the Ingress `X-Remote-User` header.
- Bind mount of `/config` so `LocalFileClient` can read + write HA YAML directly without an SMB hop.
- Options schema captures HA URL, encryption secret, license key, optional Frigate URL, optional pre-seeded LLM provider + token.
- AppArmor profile constraining Brain to its expected surface.
