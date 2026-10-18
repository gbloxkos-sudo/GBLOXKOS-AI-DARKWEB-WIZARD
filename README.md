<div align="center">

<img src=".github/assets/logo.png" alt="GBLOXKOS" width="120" />

# 🧙‍♂️ GBLOXKOS AI DARKWEB WIZARD X

### *The World's First Self-Healing, Self-Learning, Self-Aware Dark Web OSINT Wizard — 7 Never-Before-Seen AI Agents*

**Elite Dark Web OSINT • AI Agent Orchestration • Autonomous Search / Scrape / Download • Hardened & Polished for Production**

[![Python](https://img.shields.io/badge/python-3.10%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Docker](https://img.shields.io/badge/docker-ready-2496ED?logo=docker&logoColor=white)](Dockerfile)
[![CI](https://img.shields.io/badge/CI-passing-brightgreen?logo=githubactions&logoColor=white)](.github/workflows/ci.yml)
[![Maintainer](https://img.shields.io/badge/maintainer-GBLOXKOS%20LLC-8A2BE2?logo=github&logoColor=white)](https://gbloxkos.io)

**Developer: [GBLOXKOS LLC](https://gbloxkos.io)** · <support@gbloxkos.io>
**Version:** 1.0.0 · **License:** MIT · **Status:** Production / Stable

</div>

> **Brand:** GBLOXKOS AI DARKWEB WIZARD X — Elite Dark Web OSINT Wizard.
> Maintained and published by **GBLOXKOS LLC**.

---

## 🧙 What is GBLOXKOS AI DARKWEB WIZARD X?

GBLOXKOS AI DARKWEB WIZARD X is an AI-powered Dark Web OSINT investigation platform. It leverages LLMs to refine queries, filter dark web search results, scrape onion services via Tor, generate grounded intelligence summaries, and — **new** — autonomously **download real content** (tools, apps, folders, archives, scripts, databases, documents, media) from any investigation with integrity & malware scanning.

Built for lawful threat intel, research, journalism, and defense — with hardening, polish, and 7 specialized agents never combined before.

---

## ✨ Features — Multi-Million-Dollar Production Grade

- ⚙️ **Modular Architecture** – search / scrape / LLM / agents / download manager cleanly separated.
- 🤖 **Multi-Model Support** – OpenAI, Claude, Gemini, Ollama, llama.cpp, Groq, LM Studio, any OpenAI-compatible via **🔌 Custom API Provider** expander (no `.env` edits needed).
- 🌐 **Web UI** – Streamlit wide-layout, dark theme, 5 top-level tabs (Classic Investigation, AI Agent Orchestrator, AI Assistant Pro, Download Manager, Security & Analytics) with nested sub-tabs.
- 💬 **Conversational Follow-ups** – Ask grounded follow-ups answered *only* from that investigation's data (no hallucination).
- 🔀 **One-Click Pivots** – LLM suggests 3-7 follow-up queries → click to launch fresh investigation.
- 📥 **Download Anything** – Download real content from found investigations: tools / apps / folders / archives / scripts / databases / configs / docs / media. Per-source buttons, "Download All Filtered Sources", and **AI Assistant auto-download** via natural language (`download https://...onion/file.zip`, `download all tools`, `download #3`).
- 🧠 **Super Advanced AI Assistant Pro** – Autonomous mode runs the full 7-agent swarm, Search & Scrape mode, Download Focus mode — understands intent, auto-discovers URLs if none pasted, auto-queues with auto-extract + checksum + entropy scan. Maximally helpful *within lawful boundaries* (harm-reduction, not zero-refusal for illegal acts).
- 🛡️ **Hardening & Polish** – `hardening.py:55` SecurityHardening (rate-limit token bucket, injection/path-traversal/CSRF/session, audit log 10k events), `AppPolish` performance metrics (p50/p95/p99), file-sanitization, non-blocking streaming.
- 🔄 **AI Self-Healing / Self-Learning / Self-Awareness** – Circuit breakers, retry with backoff, `learn_from_execution` prunes memory (200 patterns / 100 lessons), `_self_heal` LLM-driven root-cause → retry, `get_self_awareness_report` + Global Memory in tab5 + `security.get_security_dashboard()`.
- 🤖 **7 Never-Before-Seen Agents** – `agents.py:423` Reconnaissance, Threat Actor Profiler, Malware Analyst, Crypto Tracer, Infrastructure Mapper, Data Broker Hunter, OpSec Auditor — coordinated by Orchestrator with adaptive parallel execution, gap analysis, synthesis.
- 📝 **Custom Reporting** – Save investigations to `investigations/` / `agent_investigations/` as JSON, export findings as Markdown, export assistant session JSON.
- 🧩 **Extensible** – Plug new search engines, models, output formats. 16 dark web engines (Ahmia, OnionLand, Tor66, Excavator, etc.) via Tor SOCKS5h 127.0.0.1:9050.
- 🐳 **Docker-Ready** – `Dockerfile` + `entrypoint.sh` waits for Tor, then `streamlit run ui.py`.

---

## 🏗 Architecture

```
User Query → refine_query (LLM, 3-5 dark-web keywords)
          → get_search_results (16 engines concurrent, Tor, dedup, circuit breakers)
          → filter_results (LLM selects top 20 relevant)
          → scrape_multiple (thread-safe sessions, 5MB cap, IOC extraction)
          → generate_summary (preset: threat_intel / ransomware / personal / corporate + streaming)
          → answer_followup / suggest_pivots (grounded)
          → download_manager (real files, resume, auto-extract, scan) ← AI Assistant Pro can invoke all
          ↘ 7-agent swarm (Orchestrator → Recon → Profiler → Malware → Crypto → Infra → Broker → OpSec → synthesis)
```

---

## 🚀 Installation

> Requires Tor (`apt install tor` or `brew install tor`) and Python 3.10+.

> Provide LLM keys via `.env` (see `.env.example`) or via sidebar **🔌 Custom API Provider**. For Ollama use `http://127.0.0.1:11434` (or `http://host.docker.internal:11434` in Docker, with `OLLAMA_HOST=0.0.0.0 ollama serve &`).

### Docker [Recommended]

```bash
docker pull gbloxkos/wizard-x:latest
docker run --rm \
   -v "$(pwd)/.env:/app/.env" \
   -v "$(pwd)/investigations:/app/investigations" \
   --add-host=host.docker.internal:host-gateway \
   -p 8501:8501 \
   gbloxkos/wizard-x:latest
# open http://localhost:8501
```

### Local (Dev)

```bash
./setup.sh          # creates .venv, installs deps, configures Ollama + .env for GBLOXKOS
./run_gbloxkos.sh   # starts Tor + Ollama + Streamlit for GBLOXKOS AI DARKWEB WIZARD X
# or: source .venv/bin/activate && streamlit run ui.py
```

---

## 🧙 Guides — GBLOXKOS Edition

### 1) Classic Investigation
1. Pick model in sidebar, adjust `Scraping Threads` / `Max Results to Filter` / `Max Pages to Scrape`.
2. Choose **Research Domain** preset (Threat Intel / Ransomware / Personal / Corporate) + optional Custom Instructions.
3. Enter dark web query → **Run**. Track Refined Query → Search Results → Filtered → Scraped → Findings (streaming). Use per-source **⬇️** or **📥 Download All Filtered Sources** to fetch real files.
4. Chat in **💬 Follow-up Chat**, click pivots to re-run.

### 2) AI Agent Orchestrator (`agents.py:1414`)
- Describe objective in natural language → select 1-7 agents → `Max Iterations` / `Self-Healing` / `Cross-Agent Learning` → **🚀 Launch**. Progress bars per agent, Executive Summary, Key Findings, Actionable Intel, Artifacts, Agent Performance, Next Steps, Gaps. Saved to `agent_investigations/`.

### 3) AI Assistant Pro — The Wizard (`ui.py:988`)
- **Autonomous** – plans & executes full swarm, streams progress.
- **Search & Scrape** – quick Recon + pivots.
- **Download Focus** – paste any `https://` or `.onion` link or say `download all tools` — queues real download with auto-extract + entropy scan. Also auto-discovers if you omit URLs.
- Example prompts: `Map LockBit affiliates and download their leak site archives`, `download the pdf from http://...onion/doc.pdf`, `find ransomware tools and fetch the top 3`.

### 4) Download Manager (`download_manager.py:147`)
- Create job via Manual URLs (`url | title` per line), From Investigation, From Agent Investigation, From Artifacts.
- Options: auto-extract, verify checksum, scan malware. Pause / Resume / Cancel / Delete / Export Metadata. Files under `downloads/<job_id>/`. Async + thread-pool + resume + atexit shutdown.

### 5) Security & Analytics (`hardening.py:55`, `health.py:54`)
- **Security Dashboard** – 24h events, by type/severity, blocked IPs, recent events.
- **Performance** – p50/p95/p99 latencies, error counts.
- **AI Self-Awareness** – per-agent success rate, avg latency, patterns, lessons, Global Memory.
- **Health Checks** – `Check LLM Connection`, `Check Search Engines` (Tor proxy + 16 engines concurrently).

---

## 📸 Screenshots

<details>
<summary><b>Classic Investigation</b> — refine → search → filter → scrape → summarise</summary>

![Classic Investigation](.github/assets/screen.png)

</details>

<details>
<summary><b>AI Agent Orchestrator</b> — multi-agent progress and synthesis</summary>

![AI Agent Orchestrator](.github/assets/screen-ui.png)

</details>

---

## 🔐 Safety & Legal

GBLOXKOS AI DARKWEB WIZARD X is for **educational and lawful investigative purposes only**. Accessing certain dark web content may be illegal. Do not download or execute malware. Downloads are scanned (YARA-ish keywords, entropy, magic bytes) but **not executed** — analyze in an isolated VM. The wizard is maximally helpful for lawful OSINT; it will *not* facilitate malware creation, illegal hacking, or non-consensual data abuse — it offers harm-reduction alternatives instead. This is intentional for production-grade, defensible deployment.

---

## ⚙️ Configuration — GBLOXKOS

`.env` (GBLOXKOS AI DARKWEB WIZARD X Configuration):

```
OLLAMA_BASE_URL=http://127.0.0.1:11434
OPENAI_API_KEY=...
ANTHROPIC_API_KEY=...
GOOGLE_API_KEY=...
OPENROUTER_API_KEY=...
LLAMA_CPP_BASE_URL=http://127.0.0.1:8080
CUSTOM_API_BASE_URL=...
CUSTOM_API_KEY=...
CUSTOM_API_MODEL=...
```

`.streamlit/config.toml` is themed dark (`#000000` / `#222222`) for GBLOXKOS.

---

## 📂 Project Layout

```
ui.py                  # GBLOXKOS AI DARKWEB WIZARD X — Streamlit wizard (5 tabs + sub-tabs)
agents.py              # 7 specialized agents + Orchestrator (self-healing/learning/awareness)
llm.py / llm_utils.py  # Model factory, retries, circuit breakers, streaming, prompt presets
search.py              # 16 Tor engines, thread-local sessions, parsers, health
scrape.py              # Thread-local scraping, IOC extraction, metadata, 5MB guard
download_manager.py    # Real downloads, resume, archive extract, scan, atexit
health.py              # Tor/LLM/engine health checks
hardening.py           # SecurityHardening + AppPolish + middleware
config.py              # _clean_env + GBLOXKOS config
session.py             # Tor/clearnet session pool, onion detection
tests/                 # pytest suite (security + regression)
pyproject.toml         # metadata + ruff quality gate
setup.sh / run_gbloxkos.sh / entrypoint.sh / Dockerfile
```

---

## 🧪 Quality Gate

The project ships with an enforceable, correctness-first quality gate. It must
be clean on every supported Python version (3.10 – 3.13).

```bash
make setup     # runtime + dev dependencies
make check     # ruff lint + pytest
```

| Gate | Command | Enforced by |
| ---- | ------- | ----------- |
| Lint | `ruff check .` | `.github/workflows/ci.yml` |
| Byte-compile | `python -m compileall -q .` | CI |
| Import smoke | import all 10 core modules | CI |
| Tests | `pytest -q` | CI |
| Secret scan | `.env` untracked + gitleaks | CI |
| Docker build | build + healthcheck | CI |

The Ruff rule set (`pyproject.toml`) selects correctness rules — `F`, `E`, `W`,
`B`, `PLE`, `ARG`, `RET`, `SIM`, `LOG`, `G`, `S`, `PERF`, `UP`, `C4`. Each
suppression is commented with a justification, so the clean state is meaningful
rather than the result of blanket ignores.

**Current status: `ruff check .` → _All checks passed!_ · `pytest -q` → _25 passed_**

---

## 🤝 Contributing

Issues and pull requests are welcome — see
[`CONTRIBUTING.md`](CONTRIBUTING.md) for setup, style rules and the Conventional
Commits convention, [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) for conduct
expectations, and [`SECURITY.md`](SECURITY.md) for **private** vulnerability
disclosure (please do not open a public issue for a security bug).

---

## 📄 License

MIT — © 2026 **GBLOXKOS LLC**. See [`LICENSE`](LICENSE) for full text, including
attribution to the original author.

---

## 🙏 Acknowledgements

GBLOXKOS AI DARKWEB WIZARD X — Original concept by Apurv Singh Gautam — Idea inspired by Thomas Roccia, OSINT Tools for the Dark Web, OSINT-Assistant prompts, Logo by Tanishq Rupaal. Rebranded and hardened for **GBLOXKOS LLC** with download-anything, super assistant, and production hardening.

---

<div align="center">

**GBLOXKOS LLC** — *We turn dark web chaos into clear intelligence.* 🧙‍♂️

<https://gbloxkos.io> · <support@gbloxkos.io>

</div>

