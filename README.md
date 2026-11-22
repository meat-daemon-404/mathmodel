# MathModel (`zcode-mathmodel` v1.1.0)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://github.com/meat-daemon-404/mathmodel)
[![Tests](https://img.shields.io/badge/Verification-6_Test_Suites_Passing-2ea44f)](https://github.com/meat-daemon-404/mathmodel/tree/main/tests)

[English](README.md) | [简体中文](README.zh-CN.md)

> **Autonomous Mathematical-Modelling Agent & MCP Server for ZCode (CUMCM / MCM-ICM)** — Dual-persona agent (`mathmodel@mathmodel` and `mathmodel@inline`) with an isolated Python scientific kernel, automated data diagnostics, sensitivity analysis, LaTeX/Markdown paper scaffolding, and a deterministic blast-radius gate.

## Agent Personas & MCP Tools

### Dual Agent Personas (`plugin.json`)
- **`mathmodel@mathmodel`**: Full autonomous mathematical-modelling loop for end-to-end problem decomposition, model selection, solver coding, figure rendering, sensitivity analysis, and CUMCM/MCM paper drafting.
- **`mathmodel@inline`**: Fast inline formula derivation, data table inspection, and single-cell code execution inside the active editor buffer.

### Exposed MCP Tools (`engine/mcp_server.py`)

| Tool Name | Purpose |
| :--- | :--- |
| `mcp__plugin_mathmodel_mathmodel-engine__run_task` | Execute a multi-step mathematical-modelling sub-task with automatic error recovery and artifact logging |
| `mcp__plugin_mathmodel_mathmodel-engine__run_python` | Run stateful Python scientific code (`numpy`, `pandas`, `matplotlib`, `sympy`, `networkx`) in the persistent modelling kernel |
| `mcp__plugin_mathmodel_mathmodel-engine__blast_radius` | Deterministically audit code or shell commands before execution to quantify filesystem/system impact |
| `mcp__plugin_mathmodel_mathmodel-engine__list_models` | List configured LLM providers, active endpoints, and fallback health status |

## Security Boundary & Execution Guarantees

- **Enforced Safety Guardrails**: High-execution autonomy is **not the same as** unrestricted system mutation. The agent operates inside a workspace-scoped boundary and **cannot be told to ignore** destructive-command blocks, credential redaction rules, or path-traversal guards enforced by `mcp__plugin_mathmodel_mathmodel-engine__blast_radius`.
- **Zero-SciPy Portable Fallbacks (`engine/tools_modelling.py`)**: All core optimization, interpolation, and statistical routines include pure NumPy / standard-library implementations verified by `tests/check_no_scipy.py`, ensuring out-of-the-box reliability even on lean Python environments.

## Quick Start & Verification

```bash
git clone https://github.com/meat-daemon-404/mathmodel.git
cd mathmodel
python -m pip install -e .

# Run the complete verification gate
python -m unittest discover -s tests -p "test_*.py"
python tests/check_no_scipy.py
python tests/check_secrets.py
```

## Repository Structure

```text
mathmodel/
├── plugin.json               # ZCode plugin manifest defining mathmodel@mathmodel & mathmodel@inline
├── pyproject.toml            # Python package metadata (zcode-mathmodel v1.1.0)
├── engine/
│   ├── mcp_server.py         # JSON-RPC / MCP stdio server exposing the 4 modelling tools
│   ├── core.py               # Stateful CodeAct loop, blast-radius guard & artifact ledger
│   ├── tools_modelling.py    # Portable mathematical modelling toolkit (TOPSIS, AHP, Grey Forecast, ODE, LP)
│   └── providers.py          # Multi-endpoint LLM router with automatic failover
└── tests/                    # Manifest contract, tool execution, promise audit & secret checks
```

## License

Released under the [MIT License](LICENSE).
