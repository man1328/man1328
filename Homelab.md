# Homelab Stack — The Architecture I Run

**One sentence:** I operate a self-hosted, VPN-gated, reverse-proxied stack on consumer hardware — file cloud, dashboard, AI assistant, and automation — with real backups, real monitoring, and real failure recovery.

---

## The Stack (what runs, where, why)

```
┌─────────────────────────────────────────────────────────────────────┐
│  INTERNET                                                           │
│       │                                                             │
│       ▼                                                             │
│  ┌─────────────┐     Mullvad VPN (WireGuard)      ┌──────────────┐  │
│  │  Tailscale  │◄────────────────────────────────►│  Public IP   │  │
│  │  (tailnet)  │     Encrypted egress for all     │  (rotating)  │  │
│  └──────┬──────┘     outbound traffic              └──────────────┘  │
│         │                                                          │
│         ▼                                                          │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │  HOME NETWORK (100.x CGNAT / Tailscale mesh)                 │  │
│  │                                                              │  │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐  │  │
│  │  │  Nextcloud  │  │ MagicMirror │  │      Jarvis         │  │  │
│  │  │  (files,    │  │  (dashboard │  │  (AI assistant,     │  │  │
│  │  │   photos,   │  │   on Pi)    │  │   voice, vision,    │  │  │
│  │  │   CalDAV)   │  │             │  │   automation)       │  │  │
│  │  └──────┬──────┘  └──────┬──────┘  └──────────┬──────────┘  │  │
│  │         │                │                      │            │  │
│  │         └────────────────┼──────────────────────┘            │  │
│  │                          ▼                                    │  │
│  │              ┌─────────────────────┐                          │  │
│  │              │  Docker Host        │                          │  │
│  │              │  (Ubuntu Server)    │                          │  │
│  │              │  • Ollama (LLMs)    │                          │  │
│  │              │  • Hermes Agent     │                          │  │
│  │              │  • Cron orchestration│                         │  │
│  │              └─────────────────────┘                          │  │
│  └──────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Component Breakdown

### Nextcloud — File Cloud + PIM
- **What:** Self-hosted Google Drive / iCloud replacement. Files, Photos, Contacts, Calendars, Tasks.
- **Why:** Data sovereignty. No scanning, no AI training on my photos, no subscription.
- **How it's hardened:** Mullvad VPN egress only, Tailscale for admin access, 2FA enforced, automated daily backups to off-site (encrypted rclone to B2).
- **My ops:** I run the upgrades, I debug the `occ` commands, I size the DB, I rotate the certs.

### MagicMirror² — Ambient Dashboard
- **What:** Raspberry Pi 4 driving a wall-mounted display. Modules: calendar, weather, commute, Nextcloud birthdays, Jarvis status, uptime.
- **Why:** Information radiator. Zero interaction — glanceable state.
- **My ops:** PM2 process management, config-driven module layout, auto-restart on Pi reboot, Tailscale SSH for remote edits.

### Jarvis — AI Assistant That Operates the Stack
- **What:** Python daemon (always-on) with: wake-word voice (Vosk), LLM reasoning (Ollama), YOLO vision (dog/cigar detection), Gmail notifications, Mem0+Chroma memory, Streamlit dashboard.
- **Why:** The interface layer. "Jarvis, what's the weather?" → speaks. "Jarvis, Thor near cigars?" → vision alert + email. "Jarvis, backup Nextcloud now" → triggers cron + reports result.
- **My ops:** Systemd service, structured logging → Loki, health-check cron that emails me if it dies, OAuth token refresh handled headlessly.

### Docker Host (Ubuntu) — The Compute
- **What:** Single box running Ollama (GPU), Hermes Agent (orchestration), cron jobs, all containerized.
- **Why:** One update surface, reproducible deploys, GPU passthrough for local inference.
- **My ops:** `hermes-update-watch.sh` daily cron (auto-backup + notify on new release), log rotation, disk space alerts, GPU memory monitoring.

---

## The "Invisible" Layer (what makes it production)

| Concern | Solution |
|---------|----------|
| **Secrets** | `.env` files (gitignored), 1Password CLI for CI, no secrets in images |
| **Network** | Mullvad WireGuard for all egress, Tailscale mesh for admin, no port forwards |
| **Backups** | Daily: Nextcloud DB + data → encrypted rclone → Backblaze B2. Weekly: full VM snapshot. Tested quarterly. |
| **Monitoring** | Health-check crons → email + Telegram. Loki + Grafana for logs. Uptime Kuma for HTTP endpoints. |
| **Updates** | `hermes-update-watch.sh` (daily, silent if current, auto-backup+notify on change). Host updater on laptop. |
| **Failure recovery** | Documented runbooks: "Nextcloud DB corruption," "Ollama OOM," "Mullvad handshake fail," "Pi SD card death." |

---

## What I Built vs. What I Assembled

| I Built (custom code) | I Assembled + Operate (off-the-shelf) |
|-----------------------|----------------------------------------|
| Jarvis master loop + vision guard + voice pipeline | Nextcloud (Docker), MagicMirror² (npm), Ollama |
| CLI code generator for test framework | Appium, Selenium, Allure, Jenkins |
| Hermes Agent cron orchestration + update watchdog | Docker, Tailscale, Mullvad, rclone, PM2 |
| YouTube automation pipeline (yt_manager, comment_agent) | youtube-data-api, OAuth flow |
| Job Hunter app (Streamlit multi-board scraper) | Streamlit, requests, BeautifulSoup |

---

## Failure Stories (what I've actually debugged)

- **Nextcloud DB lock** during backup → learned `occ maintenance:mode`, now backup script locks correctly.
- **Ollama OOM** on 7B model → added GPU memory limit in compose, fallback to 3B.
- **Mullvad handshake flapping** → WireGuard keepalive + systemd restart policy.
- **Jarvis Vosk false positives** ("garbage" → "Jarvis") → added secondary fuzzy-score filter, reduced wake-word list.
- **MagicMirror PM2 crash on Pi reboot** → `pm2 startup` + systemd enable, now survives power loss.
- **YouTube OAuth expiry in container** → built manual code-paste flow (`oauth_code.txt` + `oauth_state.json`) for headless refresh.

---

## What This Maps To (roles I'm targeting)

| Role | What from this stack proves it |
|------|--------------------------------|
| **QA / App Testing** | Automation Test Framework — POM, Appium, Selenium, API, Allure, Jenkins, CLI generator |
| **DevOps / SRE** | Self-hosted stack: VPN, reverse proxy, containers, backups, monitoring, runbooks, cron orchestration, update automation |
| **Application Testing** | Jarvis — voice + vision + API integration testing, flaky-test handling (Vosk), headless OAuth flow |
| **Software Engineer (test tooling)** | CLI generators, shared POM base, data-driven YAML, pytest architecture, CI pipeline design |

---

## The Interview Soundbite

> "I don't just write tests — I run the infrastructure they run on. My homelab is my sandbox: Nextcloud behind WireGuard, a Pi dashboard, an AI assistant that watches my dog and emails me, all orchestrated by cron and Hermes Agent with automated updates and tested backups. The test framework I built (Appium + Selenium + API, Allure + Jenkins, CLI generator) came from needing to test a mobile + web product *on that same infrastructure*. I know what flaky looks like because I've debugged it at 2am on my own stack."

---

## Links (when public)

- **Automation Test Framework** → `github.com/man1328/auto-test-framework`
- **Jarvis** → `github.com/man1328/my_jarvis`
- **Hermes Agent cron tooling** → `github.com/man1328/ai-stack`
- **YouTube automation** → `github.com/man1328/youtube-automation` (private, can show in interview)
- **Job Hunter** → `github.com/man1328/job-hunter` (private, can show in interview)
