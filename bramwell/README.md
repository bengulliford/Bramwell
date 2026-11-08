# Bramwell

[![Tip via PayPal](https://img.shields.io/badge/Tip%20via%20PayPal-0070BA?logo=paypal&style=flat&logoColor=white)](https://paypal.me/bengulliford)
[![Version](https://img.shields.io/badge/dynamic/yaml?url=https%3A%2F%2Fraw.githubusercontent.com%2Fbengulliford%2FBramwell%2Fmain%2Fbramwell%2Fconfig.yaml&query=%24.version&label=version&color=1f2430)](https://github.com/bengulliford/Bramwell)
![Architectures](https://img.shields.io/badge/arch-amd64%20%7C%20aarch64-1f2430)
[![Support](https://img.shields.io/badge/support-GitHub%20Issues-1f2430)](https://github.com/bengulliford/Bramwell/issues)

Alfred, an AI butler for Home Assistant. Free, runs on your own hardware, and uses the
ChatGPT, Claude, or Gemini subscription you already have.

## About

Bramwell adds a concierge dashboard to Home Assistant with Alfred inside it.

- **Chat.** Ask in plain language: lights, locks, music, the state of the house, what happened
  overnight. Alfred calls the Home Assistant API directly.
- **Voice.** Talk to Alfred through the Home Assistant voice hardware you already own, via the
  Bramwell Companion integration.
- **Automations without YAML.** Describe the automation; Alfred drafts it, shows the preview, and
  saves a real Home Assistant automation.
- **A watchful eye.** Bramwell watches the connection, the tokens, and the AI provider, and says
  so before something becomes a problem.

Everything runs on your box. Your chats go only to the AI provider you choose, with your own
keys, and Bramwell has no telemetry.

**Bramwell Pro**, the other app in this repository, adds the on-box browser agent.

## Getting started

Install, start, open the web UI, and connect your LLM provider under Settings. The
**Documentation** tab covers every option, voice setup, and where to get help.

## Support

Free is community-supported: [GitHub Issues](https://github.com/bengulliford/Bramwell/issues)
for bugs and install help, `security@bramwell.app` for security reports. Bramwell is built and
supported by one person. If Alfred earns his keep in your home, a
[tip via PayPal](https://paypal.me/bengulliford) is welcome and entirely optional.
