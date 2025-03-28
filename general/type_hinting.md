# Python Type Hinting Cheat Sheet (Python 3.9+)

## Built-in Types

```python
x: int = 42
name: str = "Alice"
price: float = 9.99
active: bool = True
```

## Collections

```python
# Lists, Tuples, Sets, Dicts (Python 3.9+ syntax)
nums: list[int] = [1, 2, 3]
names: tuple[str, str] = ("Alice", "Bob")
unique_ids: set[str] = {"a", "b", "c"}
user_ages: dict[str, int] = {"Alice": 30, "Bob": 25}
```

## Optional and Union

```python
from typing import Union

age: int | None = None  # same as Optional[int]
value: int | str = 5
```

## Type Aliases

```python
UserID = str
user_id: UserID = "abc123"
```

## TypedDict

```python
from typing import TypedDict

class User(TypedDict):
    id: int
    name: str

user: User = {"id": 1, "name": "Alice"}
```

## Custom Classes

```python
class Product:
    name: str
    price: float

p: Product = Product()
```

## Function Signatures

```python
def greet(name: str) -> str:
    return f"Hello, {name}"

def add(x: int, y: int) -> int:
    return x + y
```

## Callables

```python
from collections.abc import Callable

MathOp = Callable[[int, int], int]

def apply(op: MathOp, a: int, b: int) -> int:
    return op(a, b)
```

## Generics

```python
from typing import TypeVar, Generic

T = TypeVar("T")

class Box(Generic[T]):
    content: T

box: Box[int] = Box()
box.content = 123
```

## Literal Types

```python
from typing import Literal

Direction = Literal["N", "S", "E", "W"]

def move(direction: Direction) -> None:
    ...
```

## Annotated Types

```python
from typing import Annotated

Age = Annotated[int, "must be >= 0"]

def set_age(age: Age) -> None:
    ...
```

## Final and ClassVar

```python
from typing import Final, ClassVar

MAX_USERS: Final = 100

class Config:
    version: ClassVar[str] = "1.0"
```

## Miscellaneous

```python
from typing import Any

data: Any = get_unknown_data()

# Type checking only
from typing import TYPE_CHECKING

if TYPE_CHECKING:
    from mymodule import Something
```
