# Pydantic Cheat Sheet

## Installation

```bash
pip install pydantic
```

## Basic Model

```python
from pydantic import BaseModel

class User(BaseModel):
    id: int
    name: str
    is_active: bool = True

user = User(id=1, name="Alice")
```

## Type Coercion and Validation

```python
user = User.parse_obj({"id": "1", "name": "Alice"})  # id will be coerced to int
```

## Accessing Data

```python
user.id           # 1
user.dict()       # {'id': 1, 'name': 'Alice', 'is_active': True}
user.json()       # '{"id": 1, "name": "Alice", "is_active": true}'
```

## Required vs Optional Fields

```python
from typing import Optional

class Item(BaseModel):
    name: str
    description: Optional[str] = None
```

## Validators

```python
from pydantic import validator

class User(BaseModel):
    name: str

    @validator("name")
    def name_must_be_capitalized(cls, v):
        if not v[0].isupper():
            raise ValueError("must be capitalized")
        return v
```

## Model Inheritance

```python
class Admin(User):
    role: str = "admin"
```

## Nested Models

```python
class Address(BaseModel):
    city: str
    zip_code: str

class User(BaseModel):
    id: int
    address: Address

user = User(id=1, address={"city": "NYC", "zip_code": "10001"})
```

## Field Customization

```python
from pydantic import Field

class Product(BaseModel):
    name: str = Field(..., min_length=2)
    price: float = Field(..., gt=0)
```

## Environment Settings

```python
from pydantic import BaseSettings

class Settings(BaseSettings):
    debug: bool = False
    api_key: str

    class Config:
        env_file = ".env"
```

## Useful Methods

```python
User.parse_raw(json_string)
User.parse_file("path/to/file.json")
User.schema()
User.schema_json()
```
