# auto_comment

A simple Python tool that adds a generated `comment` column to flat files (`CSV` or `XLSX`).

It is designed for non-technical users: run one command, answer prompts, and get an output file.

## Features

- Supports input files: `.csv`, `.xlsx`
- Normalizes headers automatically:
  - trims spaces
  - lowercases text
  - removes internal spaces
  - example: ` Sales Amount ` -> `salesamount`
- Lets you define comment templates per column
- Writes output in the same format as input (`csv -> csv`, `xlsx -> xlsx`)
- Logs execution details to a file

## 1) Create virtual environment

```bash
cd auto_comment
uv venv
```

## 2) Activate virtual environment

Linux/macOS:

```bash
source .venv/bin/activate
```

Windows (PowerShell):

```powershell
.venv\Scripts\Activate.ps1
```

## 3) Install dependencies

```bash
uv pip install --python .venv/bin/python -r requirements.txt
```

## 4) Run the app

```bash
python main.py
```

## How it works

1. Enter input file path (`.csv` or `.xlsx`).
2. The app normalizes headers.
3. Enter a comment template for each column.
4. Enter the output comment column name and separator.
5. The app writes the output file.

If you leave a template blank for a column, that column is skipped.

## Template placeholders

You can use these placeholders inside each template:

- `{column}`: normalized column name
- `{value}`: current cell value
- `{row_number}`: current row index (starting from 1)

Example templates:

- for `salesamount`: `Sales={value}`
- for `region`: `Region={value}`

Result example:

```text
Sales=120 | Region=HN
```

## Logging

The app writes logs to `auto_comment.log` by default.

Log format:

```text
timestamp-log level: content
```

Actual pattern used:

```text
YYYY-MM-DD HH:MM:SS-LEVEL: message
```

Example:

```text
2026-04-22 15:10:44-INFO: Application started
```

### Custom log file path

Set environment variable `AUTO_COMMENT_LOG_FILE` before running:

```bash
AUTO_COMMENT_LOG_FILE=logs/run.log python main.py
```

## Run tests

```bash
pytest -q
```
