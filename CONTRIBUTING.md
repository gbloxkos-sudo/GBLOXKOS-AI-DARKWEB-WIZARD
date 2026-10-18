# Contributing to GBLOXKOS AI DARKWEB WIZARD X

**Developer:** GBLOXKOS LLC · <support@gbloxkos.io>
**License:** MIT

Thanks for your interest in improving Wizard X. This project handles
sensitive OSINT workflows, so contributions are reviewed carefully.

---

## Scope and conduct

This tool exists for **lawful defensive security research, threat
intelligence, journalism and education**. Contributions must preserve that
purpose. We will decline pull requests that add:

- Malware construction, weaponisation, or evasion techniques
- Credential theft, session hijacking, or persistence tooling
- Mass targeting, doxxing, or non-consensual data collection
- Capability to bypass authorisation or evade lawful detection

Features that reduce harm (detection, hardening, sanitisation, auditability,
access control) are always welcome.

---

## Development setup

```bash
git clone https://github.com/GBLOXKOS/gbloxkos-darkweb-wizard-x.git
cd gbloxkos-darkweb-wizard-x

python3 -m venv .venv
source .venv/bin/activate

pip install -r requirements.txt -r requirements-dev.txt

cp .env.example .env     # then fill in the keys you need
streamlit run ui.py
```

Tor is required for onion access:

```bash
sudo apt-get install tor     # Debian/Ubuntu
brew install tor             # macOS
```

---

## Quality gate

Every pull request must pass all three checks locally:

```bash
ruff check .                 # lint — must report "All checks passed!"
ruff format --check .        # formatting
pytest -q                    # test suite
```

Or simply:

```bash
make check
```

The CI workflow runs the same commands on Python 3.10, 3.11, 3.12 and 3.13.

---

## Code style

- Target Python **3.10+**; `from __future__ import annotations` is welcome.
- Modules are **flat top-level siblings** (`ui.py`, `llm.py`, `search.py`, …).
  They import each other with plain absolute names — do **not** introduce
  relative imports or convert the tree into a package. `__init__.py` stays a
  lightweight, lazy metadata shim for that reason.
- Line length limit is **120**.
- Every public function gets a docstring describing args, returns and raises.
- Never log secrets, API keys, session cookies, or raw investigation payloads.
- Prefer `logging` over `print()` outside CLI entrypoints.

---

## Commit messages

Use [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(agents): add passive DNS enrichment task
fix(download_manager): reject tar symlink members during extraction
docs(readme): document Ollama setup
chore(deps): bump streamlit to 1.66
```

---

## Pull requests

1. Open an issue first for anything beyond a trivial fix.
2. Keep the diff focused; unrelated refactors belong in their own PR.
3. Add or update tests that cover the change.
4. Update `README.md` if behaviour or configuration changed.
5. Fill in the PR template and request review from GBLOXKOS LLC.

---

## Reporting security issues

Do **not** open a public issue for a vulnerability. See
[`SECURITY.md`](SECURITY.md) for the private disclosure process.

---

## Licence

By contributing you agree that your work is licensed under the
[MIT License](LICENSE) and that GBLOXKOS LLC retains the copyright notice.
