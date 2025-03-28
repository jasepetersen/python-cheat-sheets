# Alembic Cheat Sheet (Database Migrations for SQLAlchemy)

## Installation

```bash
pip install alembic
```

## Initialize Alembic

```bash
alembic init alembic
```

Creates an `alembic/` directory and `alembic.ini` config file.

## Configuration

In `alembic.ini`, set your database URL:

```
sqlalchemy.url = postgresql://user:password@localhost/dbname
```

Or override it dynamically in `env.py`:

```python
from sqlalchemy import engine_from_config
from myproject.models import Base  # import your models

target_metadata = Base.metadata
```

## Create a New Migration

```bash
alembic revision -m "create users table"
```

With auto-generation:

```bash
alembic revision --autogenerate -m "add column to users"
```

## Upgrade and Downgrade

```bash
alembic upgrade head           # upgrade to latest
alembic upgrade +1             # upgrade one step
alembic downgrade -1           # downgrade one step
alembic downgrade base         # revert all migrations
```

## View History

```bash
alembic history                # list all migrations
alembic current                # show current revision
alembic heads                  # latest available revision
alembic show <revision_id>    # show details of a revision
```

## Edit a Migration Script

Each migration file includes `upgrade()` and `downgrade()` functions:

```python
def upgrade():
    op.create_table(
        'users',
        sa.Column('id', sa.Integer, primary_key=True),
        sa.Column('name', sa.String, nullable=False)
    )

def downgrade():
    op.drop_table('users')
```

## Common Operations

```python
op.create_table(...)
op.drop_table("users")

op.add_column("users", sa.Column("email", sa.String))
op.drop_column("users", "email")

op.alter_column("users", "name", nullable=False)
op.rename_table("old_name", "new_name")
op.rename_column("users", "old", "new")
```

## Branching

```bash
alembic branches     # show divergent branches
alembic merge -m "merge branches" branch1 branch2
```

## Stamp the Database

```bash
alembic stamp head   # mark the current DB as up-to-date
```

## Environment Tips

- Use `--autogenerate` with caution; always review changes before upgrading.
- Version files are located in `alembic/versions/`
- Keep metadata (`Base.metadata`) correctly set in `env.py`
