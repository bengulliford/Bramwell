# HA Add-on packaging

Backlog [#18](../docs/BACKLOG.md) — closes the install gap for HA-OS
users (the dominant install type, ~75% of HA installs per the product
spec). Without this, those users would have to downgrade to HA
Container or Compose to install Bramwell, which most won't.

This directory now holds the add-on source. The community repo
`github.com/bengulliford/bramwell-addons` is the install surface;
its `repository.yaml` points at THIS directory for the add-on
manifest and Dockerfile.

## Why the add-on is the primary distribution path

Per `business/02-PRODUCT-SPEC.md` and `business/04-RELEASE-PLAN.md`, ~75%
of HA installs run HA OS or HA Supervised, both of which install community
add-ons via a one-click flow. Add-on installs get:

- A direct bind mount of `/config` (HA's config dir) — `LocalFileClient`
  reads/writes YAML directly with no SMB hop. Set `HaConfig__Path=/config`
  in the add-on's `config.yaml` options and the existing wiring in
  `src/Bramwell.Brain/Configuration/ServiceRegistration.cs` picks it up.
- Ingress-based UI access (no port mapping, no auth wizard) — HA forwards
  authenticated requests with `X-Remote-User` headers. `AuthMiddleware.cs`
  honors that header when `Auth:TrustIngress=true`. The Docker Compose path
  is LAN-only with no login screen (self-hosted LAN-trust model); this is
  the only surface where Bramwell imposes any auth gate.
- Auto-updates via the HA add-on store.
- Multi-arch builds (amd64, aarch64) — covers Pi-class hardware.

## Files in this directory (shipped #18)

- `config.yaml` — add-on manifest (slug, version, options schema,
  `hassio_api: true`, `map: [config:rw]`, Ingress port 8080).
- `Dockerfile` — multi-stage build that compiles Brain + Concierge
  and layers .NET 10 runtime onto the HA Supervisor base image. The
  `BUILD_FROM` arg is honored for backwards-compatibility with builders
  that still pass it; the legacy `build.yaml` is no longer used per
  Supervisor 2026.04+.
- `run.sh` — bashio entrypoint. Reads add-on options and re-exports
  them as the env vars Brain's `ServiceRegistration.cs` already binds.
  Fails the add-on early with a readable message if
  `encryption_secret` is unset.
- `CHANGELOG.md` + `DOCS.md` — surfaced in the HA add-on UI.

## Companion files (separate repos)

- `repository.yaml` — sits at the root of the *separate* community repo
  `github.com/bengulliford/bramwell-addons`, not in this directory. The
  community repo's README points at this directory for the add-on
  source.
- HACS companion (`bramwell_companion`) lives at `companion/`; it
  registers Alfred as a `conversation.agent` and exposes a few sensors.

## Companion HACS integration (separate repo)

`bramwell_companion` lives in a separate custom HACS repo. It registers
Alfred as a `conversation.agent` and exposes a few sensors. Linked here
for context only — it doesn't go in this directory.

## Out of scope for this sprint (Sprint 6-8 deliverable, not now)

- Actual add-on shipment.
- HA Ingress auth wiring in `AuthMiddleware.cs`.
- The community repo at `github.com/bengulliford/bramwell-addons`.
- HA Supervisor API integration for triggering reloads from inside the
  add-on (today the Brain calls HA's REST `homeassistant.check_config`
  service, which works in both deployment modes).
