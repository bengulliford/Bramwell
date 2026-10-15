# HA Add-on packaging

Backlog [#18](../docs/BACKLOG.md) — closes the install gap for HA-OS
users (the dominant install type, ~75% of HA installs per the product
spec). Without this, those users would have to downgrade to HA
Container or Compose to install Bramwell, which most won't.

This directory is the add-on **source of truth**. The public install
surface is the separate repo `github.com/bengulliford/Bramwell`, which
carries a root `repository.yaml` plus a `bramwell/config.yaml` mirror of
this `config.yaml`. That mirrored manifest references the pre-built GHCR
image (`ghcr.io/bengulliford/bramwell-{arch}`), so Supervisor pulls the
image rather than building from a Dockerfile — the Dockerfile here is
consumed by the publish workflow, not by on-device installs.

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
  `hassio_api: true`, `map: homeassistant_config` (path `/config`),
  Ingress port 8080).
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

- `repository.yaml` + `bramwell/config.yaml` — live at the root of the
  *separate* public install repo `github.com/bengulliford/Bramwell`, not
  in this directory. That repo is publish-only; `addon/` here stays the
  source of truth, mirrored on release (same pattern as BramwellCompanion
  for the HACS integration).
- HACS companion (`bramwell_companion`) lives at `companion/`; it
  registers Alfred as a `conversation.agent` and exposes a few sensors.

## Companion HACS integration (separate repo)

`bramwell_companion` lives in a separate custom HACS repo. It registers
Alfred as a `conversation.agent` and exposes a few sensors. Linked here
for context only — it doesn't go in this directory.

## Still open / future work

The add-on has shipped (the `github.com/bengulliford/Bramwell` install
repo exists and publishes pre-built GHCR images; Ingress + `X-Remote-User`
auth are wired in `AuthMiddleware.cs`). Remaining:

- HA Supervisor API integration for triggering reloads from inside the
  add-on (today the Brain calls HA's REST `homeassistant.check_config`
  service, which works in both deployment modes).
