# SQLAlchemy Cheat Sheet

## Installation

```bash
pip install sqlalchemy
```

## Create Engine and Session

```python
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker

DATABASE_URL = "sqlite:///./test.db"

engine = create_engine(DATABASE_URL, echo=True)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
```

## Base Model

```python
from sqlalchemy.orm import declarative_base

Base = declarative_base()
```

## Define Models

```python
from sqlalchemy import Column, Integer, String

class User(Base):
    __tablename__ = "users"

    id = Column(Integer, primary_key=True, index=True)
    name = Column(String, index=True)
```

## Create Tables

```python
Base.metadata.create_all(bind=engine)
```

## Create a Record

```python
db = SessionLocal()
new_user = User(name="Alice")
db.add(new_user)
db.commit()
db.refresh(new_user)
```

## Read Records

```python
users = db.query(User).all()
user = db.query(User).filter(User.id == 1).first()
```

## Update a Record

```python
user.name = "Bob"
db.commit()
```

## Delete a Record

```python
db.delete(user)
db.commit()
```

## Relationships

```python
from sqlalchemy import ForeignKey
from sqlalchemy.orm import relationship

class Post(Base):
    __tablename__ = "posts"
    id = Column(Integer, primary_key=True)
    title = Column(String)
    owner_id = Column(Integer, ForeignKey("users.id"))

    owner = relationship("User", back_populates="posts")

User.posts = relationship("Post", back_populates="owner")
```

## Alembic for Migrations

```bash
pip install alembic
alembic init alembic
```

## Use with FastAPI Dependency

```python
from fastapi import Depends

def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
```
