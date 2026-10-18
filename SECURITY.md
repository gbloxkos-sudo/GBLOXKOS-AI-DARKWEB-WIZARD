# Security Policy

**Maintainer:** GBLOXKOS LLC · <support@gbloxkos.io>

---

## Supported versions

| Version | Supported |
| ------- | --------- |
| 1.0.x   | ✅        |
| < 1.0   | ❌        |

---

## Reporting a vulnerability

Please report vulnerabilities **privately**. Do not open a public GitHub
issue, pull request, or discussion for an unfixed vulnerability.

**Email:** <support@gbloxkos.io>
**Subject:** `[SECURITY] GBLOXKOS Wizard X — <short summary>`

Please include:

- Affected file(s) and line numbers
- Version / commit SHA
- Reproduction steps or a minimal proof of concept
- Impact assessment and any suggested remediation

You will receive an acknowledgement within **3 business days** and a triage
assessment within **10 business days**. We will coordinate disclosure timing
with you and credit you in the advisory unless you prefer otherwise.

---

## Threat model

Wizard X deliberately ingests hostile input. Understanding this model helps
you report the issues that matter.

**Untrusted by design**

- Dark web search-engine HTML
- Scraped page content from `.onion` and clearnet hosts
- Downloaded archives, binaries, scripts and databases
- LLM output, which is treated as untrusted until validated

**Assets worth protecting**

- API keys and LLM credentials (`.env`)
- Tor circuit anonymity and the local SOCKS5 proxy
- Downloaded artefacts and their integrity checksums
- Saved investigation records under `investigations/`
- The host filesystem — the app must never write outside its data directory

**Existing controls**

| Control | Location |
| ------- | -------- |
| Rate limiting, injection/CSRF/path-traversal guards, audit log | `hardening.py` |
| SSRF-safe session selection, Tor-aware routing | `session.py` |
| Download size caps, sanitised filenames | `download_manager.py` |
| Zip-Slip / symlink / device-node rejection, decompression-bomb budget | `download_manager.py` |
| Credential hygiene, `_clean_env` | `config.py` |
| Unprivileged container user, read-only-friendly layout | `Dockerfile` |

**Explicitly out of scope**

- Vulnerabilities in Tor itself, Streamlit, LangChain, or upstream libraries
  (report those upstream; we will help coordinate upgrades)
- Social engineering of the operator into misconfiguring their own deployment
- Denial of service from deliberately abusive third-party endpoints
- Findings that require an already-compromised host

---

## Responsible use

Wizard X is for lawful threat intelligence and defensive research. It does
not execute what it downloads. Analyse any retrieved artefact in an isolated
environment. See the safety section of the `README.md` for the full statement.
