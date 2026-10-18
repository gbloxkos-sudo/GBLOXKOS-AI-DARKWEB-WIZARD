# Changelog

All notable changes to **GBLOXKOS AI DARKWEB WIZARD X** are documented here.

The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] — 2026-10-17

**Developer:** GBLOXKOS LLC

First production release under GBLOXKOS LLC.

### Added

- 7 specialised OSINT agents plus an Orchestrator with adaptive parallel
  execution, gap analysis and synthesis (`agents.py`).
- Multi-provider LLM layer: OpenAI, Anthropic, Gemini, Ollama, llama.cpp and
  any OpenAI-compatible gateway, with circuit breakers, exponential-backoff
  retries and buffered streaming (`llm.py`, `llm_utils.py`).
- 16 Tor-backed dark web search engines with per-engine parsers, circuit
  breakers and deduplicated concurrent fan-out (`search.py`).
- Thread-local Tor/clearnet session management with onion detection
  (`session.py`).
- IOC extraction, content caps and streaming scrape pipeline (`scrape.py`).
- Download manager with resume, pause/cancel, integrity checksums, entropy and
  keyword malware scanning, and **hardened archive extraction** that rejects
  Zip-Slip traversal, absolute paths, symlink/hardlink escapes, device nodes
  and decompression bombs (`download_manager.py`).
- `async_download()` with a real `progress_callback` and a documented contract.
- Security hardening: rate limiting, input sanitisation, CSRF and path-traversal
  guards, audit log, p50/p95/p99 performance metrics (`hardening.py`).
- Tor, LLM and search-engine health checks (`health.py`).
- Nine-tab Streamlit UI with dark theme and streaming pipeline feedback
  (`ui.py`).
- Multi-stage, non-root, health-checked Docker image with OCI labels.
- Ruff-based quality gate in `pyproject.toml`, enforced in CI across Python
  3.10–3.13.

### Fixed

- **Security:** archive extraction used a `str.startswith()` containment check,
  which a sibling directory such as `<dest>_evil` could defeat. Replaced with
  `Path.is_relative_to()` plus absolute-path, `..`, link and special-file
  rejection, and an aggregate extraction byte budget.
- **Security:** job IDs and filename fallbacks were derived from MD5; switched
  to BLAKE2b.
- `__init__.py` used relative imports against a flat, non-package module tree,
  so it could never import successfully. Rewritten as a lazy metadata shim with
  a `load()` helper.
- `async_download()` documented progress tracking but never performed any, and
  discarded `Content-Length`; a malformed `Content-Length` header raised.
- `suggest_pivots()` accepted a `preset` argument and silently ignored it.
- `extract_onion_links()` carried a dead `base_url` parameter.
- `download_manager.shutdown()` reached `close_all_sessions` through a
  re-export chain instead of importing it from `session` directly.
- Removed dead imports across all modules, including several that were flagged
  unused but are required inside nested functions.
- Fixed `concurrent` module shadowing inside the circuit-breaker timeout path.
- Logged `exc_info` from outside an active exception handler in the pipeline
  error reporter.
- Added `raise ... from` chaining on re-raised exceptions.
- Removed redundant `f` prefixes from placeholder-free f-strings.

### Changed

- Copyright and attribution updated to **GBLOXKOS LLC**, preserving credit to
  the original author.
- Docker image moved to a two-stage build, Python 3.12 base, `tini` as PID 1 and
  a non-root `app` user.
- Lint configuration narrowed to correctness rules with documented, justified
  exemptions so the zero-error gate is meaningful rather than suppressed.

[1.0.0]: https://github.com/GBLOXKOS/gbloxkos-darkweb-wizard-x/releases/tag/v1.0.0
