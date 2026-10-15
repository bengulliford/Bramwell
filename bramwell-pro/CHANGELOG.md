# Bramwell Pro Add-on Changelog

> Bramwell and Bramwell Pro ship from one release line. Releases pro.5 through pro.15 were **Pro-only** while the free (lean) add-on stayed at 1.0.0-beta.10; from **1.0.0-\*.16** the two share one version line again — the same release ships as `beta.N` (free) and `pro.N` (Pro). Pro's history starts at `pro.3` (shipped alongside `beta.9`); earlier lean-only releases are listed in the free add-on's changelog.

## 1.0.0-pro.17 / beta.17 (2026-08-05)

- **Alfred's voice returns to the briefing** — the house's current state now opens the body (an earlier routing slip was silently dropping it), and every line is delivered in Alfred's butler register while each fact stays exactly as observed: every sentence is written about one device only, with strict checks that no reading or device name bleeds between sentences.
- **Briefing stays snappy** — the voice polish is time-boxed per line and capped per brief, so a busy house never waits on a slow model; any line that can't be polished safely appears plainly instead.

> Note: `*.16` images included an early, unhardened cut of the briefing voice. `*.17` supersedes them.

## 1.0.0-pro.16 / beta.16 (2026-08-05)

- **Latest models by default** — chat and reports now use each provider's newest flagship out of the box: Claude **Opus 5** and **Sonnet 5**, and ChatGPT **GPT-5.6 "Sol"**. You can still pick any model by name.
- **Free tier back in step** — the free Bramwell add-on rejoins the shared version line (it had been frozen at beta.10), so free-tier homes get the same up-to-date models, not last season's.
- **ARM installs get this release** — the aarch64 (ARM64) build is restored, so Raspberry Pi and other ARM boards can install alongside Intel/AMD.

## Pro 1.0.0-pro.15 (2026-08-05)

- **Briefings you can trust, word for word** — the headline is now short and factual with the details underneath (never the other way round), every house fact renders exactly as observed (the AI can no longer merge two devices into one sentence or dress up a reading), and a recurring issue appears once instead of nagging in every brief. Weather and look-ahead keep Alfred's voice.
- **Briefing settings collapsed to almost nothing** — the checkbox list and news/sports cards are gone. Everything useful is on by default (and silent when there's nothing to say); the whole surface is one who's-home switch and one optional "anything else you'd like in your briefing?" line. The heartbeat card is a single switch.
- **Cleaner prose** — no more em dashes in briefs, and finding text follows plain-language rules (one fact per sentence, one name per device, active voice).
- **Pick any AI model by name** — the provider card now has an optional model field with suggestions; type any model your subscription supports (validated with a live test when you save), so brand-new models work the day they ship.

## Pro 1.0.0-pro.14 (2026-08-04)

- **The half-hourly home check now always reads the house** — some AI providers were skipping the actual state sweep and reporting "nothing readable" while your home was fully online, which left the daily brief with no house content. Every check now starts with a verified entity count computed outside the AI, so an "empty" claim is impossible, and the check runs with more reasoning depth.
- **Briefs mention unhealthy safety devices by default** — offline or low-battery locks, alarms, cameras, garage doors, and smoke/CO sensors now appear in the brief without needing to enable the Device health card first. Healthy homes see no change (only safety devices are ever mentioned).

## Pro 1.0.0-pro.13 (2026-07-25)

- **Pick how hard Alfred thinks** — the chat model picker is now a "depth dial": ChatGPT sign-ins get Quick / Standard / Deep chips for the first time (reasoning effort — the knob ChatGPT's backend actually honors), Claude's Opus chip moves to Opus 4.8 **with extended reasoning genuinely enabled** (it previously ran with thinking off), and Gemini keeps Flash / Pro.
- **Claude reliability fixes** — two bugs found by our multi-provider test harness: tool actions taken during extended reasoning are now recorded correctly in chat history, and multi-step actions no longer stall when the model reasons silently between steps.
- **Reports use the best model your plan actually includes** — if the flagship model isn't available on your subscription, report generation steps down one tier (Opus → Sonnet, Gemini Pro → Flash) and notes it, instead of failing outright.
- **Gemini chat updated** — the Flash engine moves from a preview model to the current stable gemini-3.5-flash.

## Pro 1.0.0-pro.12 (2026-07-20)

- **Reports work with whichever AI you're signed into** — report generation now runs on your signed-in provider (ChatGPT, Claude, or Gemini) at that provider's most capable model. Previously reports required a Gemini API key, so ChatGPT and Claude sign-ins couldn't generate reports at all.
- **Cloud-tier reports are properly metered** — on hosted plans, report generation now routes through the credit proxy like every other feature, instead of running unmetered.
- **Browser-agent lockdown** — all of the agent's own control endpoints (task start/resume/cancel, confirmations, clipboard) now require the internal auth token, closing the last unauthenticated surface on the local network; an automated guard prevents any future endpoint from shipping without it.
- **Cloud plans advertise what exists** — cloud-tier manifests now list hosted LLM only; voice, browser, and backup run locally until their hosted services launch.
- **License shipped** — the repository now carries the Bramwell Source-Available License (the companion integration remains MIT).

## Pro 1.0.0-pro.11 (2026-07-05)

- **Reports now work on add-on installs** — report generation finds its Gemini key through your Primary LLM slot, so no separate key setup is needed. Previously, reports on the add-on could not run at all.
- **Sidebar & theme fixes** — the dashboard layout only flips to its embedded arrangement when it is genuinely inside the HA sidebar (no more wrong layout in standalone tabs); a stray shadow in light theme is gone.
- **Browser-agent audit trail polish** — the trail is scoped to the current task (stale rows clear when you switch tasks), starts collapsed, and screenshots open in a lightbox.

## Pro 1.0.0-pro.10 (2026-07-05)

- **Logs page overhaul** — new **System** and **Commands** tabs, a browser-agent audit trail, a log-source filter, and a Refresh button that reports what it actually fetched.
- **Sensitive values redacted** — tokens and credentials are scrubbed from the Commands and browser-task log views before anything is displayed.

## Pro 1.0.0-pro.9 (2026-07-05)

- **Dashboard fits properly inside Home Assistant** — under HA Ingress the sidebar docks to the right (HA keeps the left edge) and the top bar gains an "Open in new tab" button; standalone tabs now get a browsable link to your HA frontend instead of the unreachable internal Supervisor address.
- **Richer reports** — a "since last report" delta section, stage-based sections that keep the overall grade, a coaching tone, and stats grounded in your actual device records.
- **Support groundwork** — recent warnings are kept in a ring buffer and included in the support bundle; retention sweeps and container log caps stop logs growing without bound.

## Pro 1.0.0-pro.8 (2026-07-05)

- **Report generation hardened** — failed runs now say so instead of stalling silently; structured reports build in the background with live progress; a stuck run can no longer double-bill credits (metering-on-cancel + single-flight); report prompts make no hard-coded assumptions about your home; timestamps use your Home Assistant timezone; and when a section still can't be generated, the fallback draws on the actual conversation transcript.
- **Alfred knows the Home Assistant docs better** — ranked documentation retrieval with aliases and a local-first research protocol, so HA questions get grounded answers before Alfred reaches for the web.
- **Settings tell the truth** — module toggles now actually switch their modules off; stale settings-page claims corrected; a credential-health row on the Overview with a periodic probe. The notifications UI is hidden for v1 (the backend keeps recording).

## Pro 1.0.0-pro.7 (2026-07-05)

- **Conversations page** — a full list of your chats with search, rename, and delete (replaces the old "See all" popup).
- **Reports page** — the custom-topic report option returns, plus rename / filter / delete for saved reports; fixed custom reports rendering blank.
- **New Alfred abilities** — web search (no API key needed), stopping a running browser task, and fetching or generating your briefing on demand.
- **Chat cleanup** — raw tool-result JSON and empty bubbles no longer clutter the transcript; long-running briefing generation shows progress in the chat; the browser tab icon now matches the Bramwell site.

## Pro 1.0.0-pro.6 (2026-07-04)

- **Browser agent reaches your Home Assistant UI again** — the internal-network (SSRF) protection introduced in pro.4 was also blocking your own HA. The carve-out is restored, keyed on your actual HA host, and general web errands don't carry it.

## Pro 1.0.0-pro.5 (2026-07-04)

- **Browser agent opens the right HA URL on add-on installs** — the internal Supervisor address is mapped to your browsable HA frontend, so HA-task navigation lands on a page that actually loads.
- **Warm/cool light colors fixed on HA 2026.3+** — color temperature commands now use `color_temp_kelvin` (Home Assistant removed mired support), so temperature requests work again on newer HA versions.

## 1.0.0-beta.10 / Pro 1.0.0-pro.4 (2026-06-21)

- **Reports fixed** — the custom & structured report generators no longer fail sections with "a section could not be generated." The underlying Gemini model Google retired is fully swapped out across every path (reports, room-scan, vision, chat).
- **Encryption upgraded** — stored credentials now use AES-256-GCM, with transparent read-back of anything saved under the previous scheme (no re-entry needed).
- **Reliability & polish** — honest undo + audit-log retention fixes; light-theme status dots/borders render correctly; Ingress links no longer break under the sidebar panel.
- **Credits** — top-up webhook + "Buy more credits" for Cloud tiers; default-model pricing corrected.
- **Pro (1.0.0-pro.4)** — the browser agent now **reaches all websites and blocks only genuinely dangerous ones** (malware feeds, internal/SSRF targets, and unsafe URL schemes stay blocked). Set `BRAMWELL_BLOCK_LEGAL_CAUTION_SITES=true` to restore the previous caution list (Amazon/LinkedIn/OpenTable/gov/insurance).

## 1.0.0-beta.9 / Pro 1.0.0-pro.3 (2026-06-09)

- **Your data now survives switching between Bramwell and Bramwell Pro** — settings, license, and stored credentials live in a shared location (`/config/.bramwell`) and migrate automatically from the old `/data` home on first start. The secret + database move together or not at all, so stored credentials can never be left undecryptable; if a mixed state is detected the log explains how to recover. **Update and start this version once before installing Bramwell Pro.**
- **Modules** — install-path-aware setup hints (bundled vs install-Pro) and a hardware gate for low-RAM boxes.
- **Companion auto-deploy** — the add-on installs the bundled Bramwell Companion into `custom_components` if you don't already have it (a HACS-managed copy stays authoritative).
- **Pro (1.0.0-pro.3)** — kill switch, action audit log, screenshots, and HA-task navigation fully wired inside the single-container image (per-boot gateway token); crash-restart X cleanup fixed (`procps`); hidden founder dev-mode override.
