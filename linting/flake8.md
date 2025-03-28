# Flake8 Cheat Sheet (Python Linter)

## Installation

```bash
pip install flake8
```

## Basic Usage

```bash
flake8 script.py
flake8 .          # Lint entire project
```

## Common Options

```bash
flake8 --max-line-length=100        # Set line length limit
flake8 --exclude=migrations,venv    # Exclude specific directories
flake8 --ignore=E203,W503           # Ignore specific error codes
flake8 --count                      # Show total error count
flake8 --statistics                 # Show error code summary
```

## Error Code Categories

| Code Prefix | Category                |
|-------------|-------------------------|
| E           | Pycodestyle (PEP 8 errors) |
| W           | Pycodestyle (PEP 8 warnings) |
| F           | PyFlakes (code issues)     |
| C           | McCabe (complexity)        |
| N           | Naming issues (with plugin) |
| B           | bugbear (optional plugin)  |

## Configuration (setup.cfg or tox.ini)

```ini
[flake8]
max-line-length = 100
exclude = .git,__pycache__,migrations,venv
ignore = E203, W503
```

## Configuration (pyproject.toml with plugin support)

```toml
[tool.flake8]
max-line-length = 100
exclude = ["venv", "build"]
ignore = ["E203", "W503"]
```

## Checking Complexity

```bash
flake8 --max-complexity=10
```

## Show Source and Statistics

```bash
flake8 --show-source --statistics
```

## Use with Pre-commit

1. Create `.pre-commit-config.yaml`

```yaml
repos:
  - repo: https://gitlab.com/pycqa/flake8
    rev: 6.1.0  # Use the latest version
    hooks:
      - id: flake8
```

2. Install pre-commit hook:

```bash
pre-commit install
```

## Useful Plugins

```bash
pip install flake8-bugbear
pip install flake8-comprehensions
pip install flake8-docstrings
pip install flake8-import-order
```

## Notes

- Flake8 is extensible through plugins.
- It combines `pycodestyle`, `pyflakes`, and `mccabe`.
- Often used with `black` (format) and `isort` (imports).
- Doesn't auto-fix — it only reports issues.
