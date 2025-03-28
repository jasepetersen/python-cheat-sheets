# Black Cheat Sheet (Python Code Formatter)

## Installation

```bash
pip install black
```

Or with pre-commit:

```bash
pip install pre-commit
```

## Format a File

```bash
black script.py
```

## Format a Directory

```bash
black .
```

## Check for Changes (Dry Run)

```bash
black --check script.py
```

## Show Diffs Only

```bash
black --diff script.py
```

## Set Line Length

```bash
black --line-length 88 script.py
```

## Skip String Normalization

```bash
black --skip-string-normalization script.py
```

## Exclude Files or Directories

```bash
black --exclude "/migrations/" .
```

## Include Only Certain Files

```bash
black --include '\.pyi?$' .
```

## Format Jupyter Notebooks

```bash
black notebook.ipynb
```

## Format from Standard Input

```bash
cat script.py | black -
```

## Configuration File (pyproject.toml)

```toml
[tool.black]
line-length = 100
target-version = ['py39']
skip-string-normalization = true
exclude = '''
/(
    \.eggs
  | \.git
  | \.migrations
  | \.venv
)/
'''
```

## Target Python Versions

```bash
black --target-version py38 script.py
black --target-version py311 script.py
```

## Use with Pre-commit

1. Create `.pre-commit-config.yaml`

```yaml
repos:
  - repo: https://github.com/psf/black
    rev: 23.3.0  # Use latest tag
    hooks:
      - id: black
```

2. Install pre-commit hook:

```bash
pre-commit install
```

## VS Code Integration

- Install "Python" extension
- Add to settings.json:

```json
"python.formatting.provider": "black",
"editor.formatOnSave": true
```

## Notes

- Black is uncompromising and opinionated.
- It formats your code consistently, reducing bikeshedding.
- If Black changes your file, it's because it wasn't compliant.
