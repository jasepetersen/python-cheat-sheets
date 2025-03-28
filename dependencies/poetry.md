# Poetry Cheat Sheet (Python Dependency Management & Packaging)

## Installation

```bash
curl -sSL https://install.python-poetry.org | python3 -
```

Add Poetry to your PATH if needed:

```bash
export PATH="$HOME/.local/bin:$PATH"
```

Check version:

```bash
poetry --version
```

---

## Create a New Project

```bash
poetry new my_project
```

Creates:

```
my_project/
├── pyproject.toml
├── my_project/
│   └── __init__.py
└── tests/
```

---

## Use in Existing Project

```bash
cd my_project
poetry init
```

---

## Add Dependencies

```bash
poetry add requests
poetry add fastapi@^0.110.0
poetry add numpy --extras "mkl"
```

Add dev dependencies:

```bash
poetry add --dev black pytest
```

---

## Remove Dependencies

```bash
poetry remove requests
```

---

## Install All Dependencies

```bash
poetry install
```

---

## Update Dependencies

```bash
poetry update
```

---

## Lock File

```bash
poetry lock     # Regenerates poetry.lock
```

---

## Run Commands Inside Env

```bash
poetry run python script.py
poetry run pytest
```

---

## Spawn a Shell in the Env

```bash
poetry shell
```

Exit with `exit` or `Ctrl-D`.

---

## Check Dependencies

```bash
poetry show         # Installed packages
poetry show --tree  # Dependency tree
```

---

## Virtual Environment Location

```bash
poetry env info
poetry env list
```

---

## Export Requirements for pip

```bash
poetry export -f requirements.txt --output requirements.txt
```

---

## Build Package

```bash
poetry build
```

Creates `.tar.gz` and `.whl` in `dist/`.

---

## Publish to PyPI

```bash
poetry config pypi-token.pypi your-token
poetry publish --build
```

---

## Configuration

Set config values:

```bash
poetry config --list
poetry config virtualenvs.in-project true
```

---

## pyproject.toml Example

```toml
[tool.poetry]
name = "my_project"
version = "0.1.0"
description = "Example package"
authors = ["Your Name <you@example.com>"]

[tool.poetry.dependencies]
python = "^3.10"
requests = "^2.31.0"

[tool.poetry.dev-dependencies]
pytest = "^7.0"
black = "^23.0"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"
```

---

## Notes

- Poetry uses `pyproject.toml` instead of `requirements.txt`.
- Automatically creates and manages virtual environments.
- Ideal for modern Python projects and publishing packages.
