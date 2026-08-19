[Download PDF](https://github.com/man1328/man1328/releases/download/v1.0/RESUME.pdf)

# Hi, I'm Manny 👋

**DevOps-leaning platform engineer building self-hosted AI infrastructure, automation frameworks, and tools that solve real problems I've had.**

Currently operating a full local AI stack (Ollama, RAG, agent gateway, coding agents) on consumer hardware with production-grade automation, and looking to bring that same "make infrastructure reliable" mindset to a team that values **shipping, not just writing**.

---

## 🔧 What I Do

| Domain | Evidence |
|--------|----------|
| **DevOps / Platform** | Self-hosted Nextcloud, MagicMirror, AI stack — VPN-gated, reverse-proxied, auto-updating with rollback |
| **QA / App Testing** | Built a multi-layer (Appium + Selenium + API) test framework with Allure + Jenkins CI and a CLI project generator |
| **Automation** | Cron-orchestrated scraping, AI enrichment, YouTube content pipeline, AI-assisted code generation |
| **Local AI / MLOps** | GPU LLM serving (6GB VRAM), RAG (ChromaDB), embedding search, agent delegation |

---

## 🚀 Featured Work

### 🧪 [auto-test-framework](https://github.com/man1328/auto-test-framework)
**Multi-layer automation testing framework** — Appium (Android) + Selenium (Web) + `requests` (API), unified Page Object Model, Allure + Jenkins CI, Jinja2-powered CLI that scaffolds entire test projects in seconds.

> **Why it matters:** Most testing tools are single-layer. This one runs all three from a shared codebase with a code generator that eliminates boilerplate.

### 🏠 [my_jarvis](https://github.com/man1328/my_jarvis)
**Always-on AI home assistant** — wake-word voice (Vosk), local LLM reasoning (Ollama), YOLOv8 vision (custom-trained for my dog + cigar detection), Gmail notifications, persistent memory (Mem0 + ChromaDB), Streamlit dashboard.

> **Why it matters:** Demonstrates end-to-end ML integration — speech → intent → action → memory → response — running reliably as a long-lived daemon.

### 📋 [Streamlit Job Hunter](https://github.com/man1328/Streamlit-Contained)
**Multi-board job search platform** — scrapes LinkedIn, Indeed, Glassdoor, ZipRecruiter; enriches with local Ollama; tracks applications through a Kanban board; generates tailored interview prep; ships a daily email digest via cron.

> **Why it matters:** Built because existing tools don't talk to each other. Production data flow: scrape → enrich → track → prep → apply — all Dockerized, all local-first.

### 🐳 [ai-stack](https://github.com/man1328/ai-stack)
**Self-hosted AI platform** — Ollama (GPU), Odysseus (RAG workspace), Hermes (agent gateway), OpenCode (coding agent), SearXNG, ChromaDB, ntfy, MusicGen, Telegram bots. All Dockerized with NVIDIA passthrough, automated updates, health checks, and rollback on failure.

> **Why it matters:** Real infrastructure work — VPN networking, GPU memory budgeting, automated rollback, config guards after schema migrations. This is the stack that powers the other three projects.

---

## 🛠️ Stack at a Glance

**Languages:** Python · Bash · YAML · Markdown · a little JS/TS
**Infra:** Docker, Docker Compose, systemd, WireGuard, Tailscale, Nginx
**Cloud:** AWS (S3, EC2 basics), rclone, Backblaze B2
**Testing:** Pytest, Selenium 4, Appium 2, Allure, Jenkins, Playwright
**AI/ML:** Ollama, ChromaDB, Mem0, Vosk, YOLOv8, OpenAI API
**Data:** SQLite, ChromaDB, RAG, semantic search, BeautifulSoup
**Ops:** Cron orchestration, health monitoring, automated rollback, systemd services

---

## 🏠 What I Operate (Homelab)

- **Nextcloud** behind Mullvad VPN — my file cloud + PIM
- **MagicMirror²** on Raspberry Pi — ambient dashboard
- **AI Stack** on Ubuntu + RTX A3000 — local LLMs, agents, music generation
- **Automated updates** — Mon/Thu 9 AM cron pulls new releases, backs up state, rolls back on failure
- **Off-site encrypted backups** — daily rclone to B2

*I don't just write code — I run production. I know what flaky looks like because I've debugged it at 2am on my own stack.*

---

## 🎯 Looking For

**Roles where I can apply:** platform engineering, DevOps, SRE, QA automation, test tooling, infrastructure-as-code, or anything involving "make reliable systems that do useful things."

**Open to:** Remote, hybrid, or relocation (Virginia / Florida preferred). Available immediately.

---

## 📫 Contact

- **Email:** maguilar1310@gmail.com
- **GitHub:** [github.com/man1328](https://github.com/man1328)
- **Resume:** [Download PDF](https://github.com/man1328/man1328/releases/tag/resume) (pinned release)
- **This page:** [github.com/man1328](https://github.com/man1328)

---

## 📊 GitHub Stats

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=man1328&show_icons=true&theme=default&hide_border=true)
![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=man1328&layout=compact&theme=default&hide_border=true)

---

*Last updated: August 2026*
*This README is auto-curated — if a repo here looks stale, ping me, it's probably private and I can grant read access on request.*
