# Python Language Basics Cheat Sheet

## Variables

```python
x = 42
name = "Alice"
pi = 3.14
is_active = True
```

## Functions

```python
def greet(name):
    return f"Hello, {name}"

def add(a, b=0):
    return a + b
```

## Lambda Functions

```python
square = lambda x: x * x
add = lambda a, b: a + b

print(square(4))  # 16
```

## Classes and Objects

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        return f"Hi, I'm {self.name}"

alice = Person("Alice", 30)
print(alice.greet())  # Hi, I'm Alice
```

## Inheritance

```python
class Employee(Person):
    def __init__(self, name, age, position):
        super().__init__(name, age)
        self.position = position
```

## List Comprehension

```python
squares = [x * x for x in range(10)]
evens = [x for x in range(10) if x % 2 == 0]
```

## Dictionary Comprehension

```python
squares = {x: x * x for x in range(5)}
even_map = {x: "even" for x in range(10) if x % 2 == 0}
```

## Looping

```python
for i in range(5):
    print(i)

while True:
    break
```

## Conditionals

```python
x = 10
if x > 0:
    print("Positive")
elif x == 0:
    print("Zero")
else:
    print("Negative")
```

## Built-in Data Types

```python
# List
fruits = ["apple", "banana", "cherry"]

# Tuple
point = (1, 2)

# Set
unique_values = {1, 2, 3}

# Dictionary
person = {"name": "Alice", "age": 30}
```

## Truthy and Falsy

Falsy values include:
- `None`
- `False`
- `0`, `0.0`
- `''` (empty string)
- `[]`, `{}`, `set()` (empty collections)

```python
if not []:
    print("Empty list is falsy")
```

## Importing Modules

```python
import math
from datetime import datetime
```

## Docstrings

```python
def multiply(a, b):
    """Multiply two numbers."""
    return a * b
```

## Annotations (Type Hints)

```python
def divide(a: float, b: float) -> float:
    return a / b
```

## The `__main__` Check

```python
if __name__ == "__main__":
    print("Running as script")
```
