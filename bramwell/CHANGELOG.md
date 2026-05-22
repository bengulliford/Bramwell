# Bramwell Add-on Changelog

## 1.0.0-beta.3 (2026-05-15)

- First add-on release. Backlog [#18](../docs/BACKLOG.md) closes the install gap for HA-OS users.
- Multi-arch base images (`amd64`, `aarch64`).
- HA Ingress UI; Bramwell auth gate trusts the Ingress `X-Remote-User` header.
- Bind mount of `/config` so `LocalFileClient` can read + write HA YAML directly without an SMB hop.
- Options schema captures HA URL, encryption secret, license key, optional Frigate URL, optional pre-seeded LLM provider + token.
- AppArmor profile constraining Brain to its expected surface.
