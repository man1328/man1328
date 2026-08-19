# Resume — Manuel "Manny" Aguilar

**Email:** maguilar1310@gmail.com | **GitHub:** [github.com/man1328](https://github.com/man1328) | **Location:** Elizabeth, NJ (open to remote / VA / FL)

---

## Summary

Platform-minded engineer with a self-taught, production-grade background in **DevOps automation, QA tooling, and self-hosted AI infrastructure**. I don't just write code — I operate the systems it runs on (Docker, GPU workloads, WireGuard, cron orchestration, automated rollback). Most comfortable shipping end-to-end: from a CLI that scaffolds test projects, to the AI-assisted debugging at 2am on my own stack. Looking for a team that values **shipping reliable systems**, not just producing tickets.

---

## Skills

| Category | Tools |
|----------|-------|
| **Languages** | Python (primary), Bash, YAML, Markdown, basic JS/TS |
| **DevOps / Infra** | Docker, Docker Compose, systemd, WireGuard (Mullvad), Tailscale, Nginx, rclone, cron orchestration |
| **CI/CD** | Jenkins (declarative pipelines), GitHub Actions basics, automated rollback, config guards |
| **Testing** | Pytest, Selenium 4, Appium 2, Playwright, Allure, Jenkins, POM architecture, data-driven YAML |
| **AI / ML** | Ollama (local LLM serving), ChromaDB (RAG), Mem0, Vosk (offline STT), YOLOv8 (custom training), MusicGen |
| **Cloud** | AWS S3/EC2 basics, Backblaze B2, S3-compatible storage, encrypted backups |
| **Data** | SQLite, ChromaDB embeddings, semantic search, BeautifulSoup, multi-source scraping |
| **Networking** | VPN tunneling, SMB/NFS mounts, reverse proxies, DNS, port security, GPU passthrough |
| **OS** | Ubuntu Server (daily driver), Linux CLI, systemd services, package management |

---

## Projects

### 🧪 [auto-test-framework](https://github.com/man1328/auto-test-framework) — `Python · Pytest · Selenium · Appium · Allure · Jenkins`

**Multi-layer automation testing framework** — Appium (Android) + Selenium (Web) + `requests` (API), unified Page Object Model, Allure + Jenkins CI, Jinja2-powered CLI that scaffolds entire test projects in seconds.

**Highlights:**
- Designed multi-layer architecture: shared POM base classes, YAML data-driven tests, unified `.env` config
- Built CLI code generator (Jinja2 templates) that scaffolds complete test projects in <30 sec — interactive or one-liner
- Wired Allure + JUnit + Jenkins declarative pipeline end-to-end with Allure/JUnit publishing
- Implemented `pytest-rerunfailures` (auto-retry flaky tests), `pytest-xdist` (parallel execution), severity/feature annotations
- API example project runs immediately with zero external deps — proof of zero-config usability

### 🏠 [my_jarvis](https://github.com/man1328/my_jarvis) — `Python · Vosk · Ollama · YOLOv8 · Mem0 · Streamlit`

**Always-on AI home assistant** integrating wake-word voice (Vosk), local LLM reasoning (Ollama), YOLOv8 computer vision (custom-trained for dog/cigar detection), Gmail notifications, and persistent memory (Mem0 + ChromaDB).

**Highlights:**
- Designed master daemon loop: voice capture → STT → intent → LLM → action → memory → TTS
- Integrated 5+ ML subsystems into one process: Vosk (offline STT), Ollama (LLM), YOLOv8 (vision), Mem0 (memory), TTS
- Built Streamlit dashboard with live camera feed, command log, session counters, one-click triggers
- Implemented Levenshtein-based wake-word fuzzy filter — cut Vosk false positives by ~90%
- Wired systemd service + health-check cron with email alerting on daemon death
- Trained custom YOLO classes on ~200 labeled frames; runs ~15 FPS on RTX A3000 6GB

### 📋 [Job Hunter (Streamlit)](https://github.com/man1328/Streamlit-Contained) — `Python · Streamlit · Playwright · Ollama · Docker`

**Multi-board job search platform** that scrapes LinkedIn, Indeed, Glassdoor, ZipRecruiter; enriches with local Ollama; tracks applications through a Kanban board; generates tailored interview prep; ships a daily email digest via cron.

**Highlights:**
- Built end-to-end pipeline: scrape → deduplicate → AI-enrich → track → prep → apply (single Docker container)
- Multi-board scraping with shared base class + per-site selectors (Playwright + ScraperAPI + FlareSolverr)
- Local Ollama enrichment for fit scoring, requirement extraction, cover letter generation — zero cloud cost
- Daily cron → `docker exec` → scrape → enrich → HTML email digest at 8 AM
- ChromaDB semantic search: "find jobs similar to this one I liked"
- Streamlit Kanban UI: Applied → Screening → Interview → Offer → Rejected with notes/dates/contacts

### 🐳 [ai-stack](https://github.com/man1328/ai-stack) — `Docker · Ollama · NVIDIA · WireGuard · Bash`

**Self-hosted AI platform** with 10+ containerized services: Ollama (GPU LLM serving), Odysseus (RAG workspace), Hermes (agent gateway), OpenCode (coding agent), SearXNG, ChromaDB, ntfy, MusicGen, Telegram bots.

**Highlights:**
- Built automated update system with backup, apply, verify, rollback on failure, Telegram notification (`check-updates.sh`)
- Built config guards (`ensure-hermes-config.py`, `ensure-odysseus-endpoints.py`) that re-assert critical config after schema migrations
- Solved VPN + Docker DNS conflicts by running Ollama on `network_mode: host` + `host.docker.internal` bridge
- Built systemd cleanup service that kills stale host processes on boot before Docker starts
- Tuned GPU memory for 6GB VRAM: `qwen2.5:7b` default (5GB), 13B+ offloads to RAM, profile-gated ACE-Step (disabled)
- Multi-bot Telegram gateway (Odysseus + Hermes) with model switching (`/local`, `/cloud`), 290-provider OmniRoute fallback

---

## Homelab / Personal Infrastructure

I operate a self-hosted, VPN-gated, reverse-proxied stack on consumer hardware:

| Service | Purpose | My Contribution |
|---------|---------|-----------------|
| **Nextcloud** (Docker, behind Mullvad VPN) | File cloud + PIM | Deploy, upgrade, backup, DB maintenance |
| **MagicMirror²** (Pi 4 + PM2) | Ambient dashboard | Config, modules, auto-restart on reboot |
| **AI Stack** (Ubuntu + RTX A3000) | Local LLMs, RAG, agents | Full orchestration + automation |
| **Tailscale mesh** | Secure admin access | All services accessible only via tailnet |
| **rclone → Backblaze B2** | Encrypted off-site backups | Daily cron, tested quarterly |
| **Cron orchestration** | Automation backbone | 10+ jobs, health checks, error alerting |

**Notable incidents debugged:**
- Ollama OOM on 7B → GPU memory limit + 3B fallback in compose
- Vosk false positives ("garbage" → "Jarvis") → Levenshtein filter on candidates
- Mullvad handshake flapping → WireGuard keepalive + systemd restart policy
- Nextcloud DB lock during backup → `occ maintenance:mode` in backup script
- MagicMirror PM2 crash on Pi reboot → `pm2 startup` + systemd enable
- YouTube OAuth expiry in container → manual code-paste flow for headless refresh

---

## Experience

### [Your Most Recent Role — Tweak or Remove]
**[Job Title]** | [Company] | [Start Date] – [End Date] | [Location]

- [Achievement with concrete outcome, e.g., "Reduced average test execution time by 40% by implementing parallel execution via pytest-xdist"]
- [System you built/operated, e.g., "Maintained CI/CD pipeline serving 50+ engineers, including nightly regression and weekly Allure reports"]
- [Cross-functional work, e.g., "Collaborated with product team to define acceptance criteria for 8 feature releases"]

### [Previous Role — Tweak or Remove]
**[Job Title]** | [Company] | [Start Date] – [End Date] | [Location]

- [Achievement with numbers: "Reduced manual QA time by X hours/week by automating Y test cases"]
- [Tech you owned: "Owned end-to-end delivery of internal tooling serving N users"]
- [Problem you solved: "Diagnosed and resolved intermittent build failures caused by Z dependency"]

---

## Education

**[Your Degree]** — [University] | [Year]

---

## Certifications (Optional)

- [List any certs you have, or remove section]

---

## Open Source Contributions

- [Project name + link + one-line description]
- [Project name + link + one-line description]

---

## How to Reach Me

- **Email:** maguilar1310@gmail.com
- **GitHub:** [github.com/man1328](https://github.com/man1328) (best for code review / portfolio)
- **Response time:** Usually within 24 hours

---

*Last updated: August 2026. Reference repositories above for proof of work; happy to grant read access to private repos on request.*
