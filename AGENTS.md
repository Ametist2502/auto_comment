# Repository Guidelines

## Project Structure & Module Organization
This repository is a small Python CLI tool for adding Excel header comments.
- `main.py`: application entry point and core logic (file loading, header normalization, comment writing, logging).
- `tests/test_main.py`: pytest suite covering normalization, CSV/XLSX loading, output generation, and logging behavior.
- `data/`: sample or working input/output files used during local runs.
- `requirements.txt`: runtime and test dependencies.
- `auto_comment.log`: default runtime log file (generated at execution time).

Keep new code in focused functions inside `main.py` unless complexity justifies splitting into modules.

## Build, Test, and Development Commands
Set up environment and dependencies:
```bash
uv venv
source .venv/bin/activate
uv pip install --python .venv/bin/python -r requirements.txt
```
Run the CLI locally:
```bash
python main.py
```
Run tests:
```bash
pytest -q
```
Use custom log destination when needed:
```bash
AUTO_COMMENT_LOG_FILE=logs/run.log python main.py
```

## Coding Style & Naming Conventions
- Follow PEP 8 with 4-space indentation.
- Use type hints (`list[str]`, `dict[str, str]`) consistently, matching existing code.
- Prefer descriptive `snake_case` for variables/functions (`normalize_headers`, `write_xlsx_with_header_comments`).
- Keep functions single-purpose and side effects explicit (I/O, logging, user prompts).

## Testing Guidelines
- Framework: `pytest`.
- Add tests in `tests/test_*.py`; name test functions as `test_<behavior>()`.
- Cover both happy paths and validation/error paths (e.g., duplicate normalized headers, invalid input files).
- For CLI flows, use `monkeypatch` and `tmp_path` as in current tests.

## Commit & Pull Request Guidelines
Recent history shows short, direct commit messages (e.g., `update config`, `Update README.md with script usage instructions`).
Prefer clearer imperative messages:
- `fix: validate duplicate normalized headers`
- `test: add xlsx comment writing coverage`

For pull requests:
- Describe what changed and why.
- Reference related issue/task IDs when available.
- Include test evidence (`pytest -q` output summary).
- For CLI behavior changes, include a short example of new prompts/output.
