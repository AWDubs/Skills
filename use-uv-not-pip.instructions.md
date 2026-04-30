---
description: "Always use uv instead of pip for Python package and environment management. Use when: installing Python packages, creating virtual environments, running Python scripts/tools, managing dependencies, working with pyproject.toml/requirements.txt, or suggesting any pip/python -m venv/pipx command."
applyTo: "**/*.py,**/pyproject.toml,**/requirements*.txt,**/uv.lock,**/.python-version"
---

# Use `uv` Instead of `pip` (Always)

`uv` is the required tool for all Python package and environment management. Never suggest or run `pip`, `pip3`, `python -m pip`, `python -m venv`, `virtualenv`, `pipx`, or `poetry` commands.

## Command Mapping

| Don't use | Use instead |
|-----------|-------------|
| `pip install <pkg>` | `uv add <pkg>` (in a project) or `uv pip install <pkg>` (ad hoc) |
| `pip install -r requirements.txt` | `uv pip install -r requirements.txt` or `uv sync` |
| `pip uninstall <pkg>` | `uv remove <pkg>` |
| `pip list` / `pip freeze` | `uv pip list` / `uv pip freeze` |
| `python -m venv .venv` | `uv venv` |
| `pipx run <tool>` | `uv tool run <tool>` (alias: `uvx <tool>`) |
| `pipx install <tool>` | `uv tool install <tool>` |
| `python script.py` | `uv run script.py` |
| `python -m <module>` | `uv run python -m <module>` |

## Rules

- Prefer project workflows (`uv add`, `uv sync`, `uv run`) over `uv pip ...` when a `pyproject.toml` exists.
- Never activate a venv manually before running commands — use `uv run` so the correct environment is selected automatically.
- For one-off CLI tools, use `uvx <tool>` instead of installing globally.
- If a `requirements.txt` is the only dependency manifest, use `uv pip install -r requirements.txt` against a `uv venv`.
- When writing setup docs or READMEs, all install/run instructions must use `uv`.

## Self-check Before Responding

If a planned command contains `pip`, `venv`, `virtualenv`, `pipx`, or `poetry`, rewrite it using the table above before sending or executing it.
