# pip + venv Cheat Sheet (Python Packaging & Virtual Environments)

## Check pip Version

```bash
pip --version
```

## Upgrade pip

```bash
pip install --upgrade pip
```

---

## Virtual Environments (`venv`)

### Create Virtual Environment

```bash
python -m venv venv
```

### Activate Virtual Environment

- **Unix/macOS:**

```bash
source venv/bin/activate
```

- **Windows:**

```bash
venv\Scripts\activate
```

### Deactivate Environment

```bash
deactivate
```

---

## Installing Packages

```bash
pip install requests
```

### Specific Version

```bash
pip install requests==2.31.0
```

### Minimum Version

```bash
pip install requests>=2.0
```

### Multiple Packages

```bash
pip install flask sqlalchemy psycopg2
```

---

## Freeze Dependencies

```bash
pip freeze > requirements.txt
```

## Install from Requirements File

```bash
pip install -r requirements.txt
```

---

## Uninstall a Package

```bash
pip uninstall flask
```

## List Installed Packages

```bash
pip list
```

## Show Package Info

```bash
pip show requests
```

---

## Search Packages (Deprecated in newer pip)

```bash
pip search flask  # May be disabled in latest pip
```

Use https://pypi.org/ for package discovery instead.

---

## Installing from a Git Repo

```bash
pip install git+https://github.com/psf/requests.git
```

---

## Editable Installs (for local development)

```bash
pip install -e .
```

---

## Installing a Local Package

```bash
pip install ./mypackage
```

---

## Upgrading a Package

```bash
pip install --upgrade flask
```

---

## Cache Directory

```bash
pip cache dir
pip cache list
pip cache purge
```

---

## Notes

- Always use a virtual environment for project isolation.
- Combine with tools like `black`, `flake8`, and `pre-commit` for clean development workflows.
- Use `requirements.txt` or `pyproject.toml` for reproducible environments.
