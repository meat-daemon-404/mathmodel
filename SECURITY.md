# Security & Publish Gate Policy (`tests/check_secrets.py`)

## 1. Zero-Exemption Self-Proving Secret & Identity Scanner

`mathmodel` ships a self-proving security and privacy gate (`python3 tests/check_secrets.py --worktree`) that enforces strict hygiene before any commit or release:

- **No Self-Exemption**: The scanner file (`tests/check_secrets.py`) holds zero path or keyword exemptions for itself. Selftest fixtures are assembled dynamically at runtime via concatenation so a genuine leaked secret on a line containing `re.compile` is never silently ignored.
- **Tracked + Untracked Coverage**: Worktree mode scans `git ls-files --cached --others --exclude-standard`, catching untracked files before they are staged.
- **Covered Signatures**:
  - API keys, bearer tokens, and private key PEM blocks (`PRIVATE KEY`)
  - POSIX and Windows local user paths (`/Users/<name>`, `C:\Users\<name>`)
  - Machine hostname shapes (`\b[a-z]+-[a-z]+-\d{2,}\b`)

## 2. Running the Gate Locally

```bash
python3 tests/check_secrets.py --worktree
python3 -m unittest discover -s tests
```

## 3. Reporting Vulnerabilities

Please report security issues via GitHub Security Advisories at `https://github.com/meat-daemon-404/mathmodel/security/advisories/new`.
