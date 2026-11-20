# Changelog

All notable changes to **mathmodel** (`meat-daemon-404/mathmodel`) are documented in this file.

## [1.1.0] - 2026-11-20

### Added
- **PEP 621 Standard Packaging (`pyproject.toml`)**: Added declarative Python project metadata, optional `scipy`/`sympy`/`pandas` extras (while preserving the `scipy`-free fallback path verified in CI), and package discovery for `engine.*`.
- **Security & Governance Documentation (`SECURITY.md`, `CHANGELOG.md`)**: Documented the zero-exemption, self-proving credential and machine-identity publish gate (`tests/check_secrets.py`).

## [1.0.0] - 2026-10-16

### Added
- **Autonomous Mathematical Modelling Engine (`engine/`)**: Numerical solver, sensitivity validator, publication figure plotter, and LaTeX/Markdown paper drafter for ZCode (`.zcode-plugin`) and Claude Code (`.claude-plugin`) with zero mid-loop confirmation pauses.
- **Self-Proving Secret & Identity Publish Gate (`tests/check_secrets.py`)**: Scans working tree (`--worktree`, including untracked files) and full Git history for credentials, private keys, local user paths, and machine hostnames with derived history waivers and 4-suite CI matrix (including a `scipy`-free runner).
