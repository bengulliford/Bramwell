# Bramwell Support

If something has gone wrong, please include a **support bundle** with your report. The bundle is a single redacted text dump that captures the running build, container health, license tier, and the most relevant diagnostic state — without your HA token, OAuth bearers, API keys, or saved passwords.

## Generating a support bundle

**From the dashboard:**

1. Open Settings → Support.
2. Click **Copy support bundle**.
3. Paste it into your bug report (a GitHub issue, or email for security reports).

**From the command line:**

```sh
curl -s http://YOUR_BRAMWELL_HOST/api/support/bundle > bramwell-support.txt
```

The endpoint returns plain text; `>` redirects it to a file you can attach.

## What the bundle contains

- **Version** — running build's version + commit SHA.
- **Runtime** — .NET version, OS / architecture, machine name.
- **Service health** — HA WebSocket, browser-agent, database, Frigate, Whisper, Kokoro (each marked healthy / unhealthy with the redacted reason on failure).
- **License** — tier, modules enabled, expiry, fallback flag. **No license key.**
- **Configured** — the list of services Bramwell believes are configured on this install.

## What the bundle does NOT contain

- Your HA long-lived access token.
- LLM API keys (Anthropic, OpenAI, Gemini).
- OAuth refresh tokens / bearer headers.
- Saved passwords / form values from the browser agent.
- Screenshots from past browser-agent tasks.
- Conversation history with Alfred.

The redactor strips token-shaped substrings (Bearer headers, `sk-…` keys, JWTs, `password=…` / `token=…` / `secret=…` assignments) before the bundle leaves your host. If you spot anything secret-looking that survived redaction, **stop, redact it manually, and open a security report** before pasting the bundle anywhere public.

## Where to send a report

- **Questions / install help:** ask in [GitHub Discussions](https://github.com/bengulliford/Bramwell/discussions) — the free tier is community-supported, so Discussions is where answers accumulate. Use the Q&A category so a reply can be marked as the answer.
- **Bugs:** open an issue at [github.com/bengulliford/Bramwell/issues](https://github.com/bengulliford/Bramwell/issues) with a support bundle attached.
- **Security:** `security@bramwell.app`. Do not post secrets or exploit details in a public issue or thread.
- **Feature requests:** the Ideas category in Discussions, or the issue tracker labelled `enhancement`.

## Versions

Both `/api/support/bundle` and the Settings → Support card landed in v1.0 as part of Backlog #36. The redactor is intentionally narrow — see `SupportEndpoints.Redact` for the exact regex set so you can audit it before sharing the bundle in a sensitive context.
