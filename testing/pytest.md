# Pytest Cheat Sheet

## Installation

```bash
pip install pytest
```

## Basic Test Function

```python
def test_addition():
    assert 1 + 1 == 2
```

## Run Tests

```bash
pytest
```

Run a specific file:

```bash
pytest test_file.py
```

Run a specific test function:

```bash
pytest -k "test_function_name"
```

## Assertions

```python
assert x == y
assert x in y
assert x > y
assert isinstance(x, MyClass)
```

## Grouping Tests with Classes

```python
class TestMath:
    def test_add(self):
        assert 1 + 1 == 2

    def test_subtract(self):
        assert 2 - 1 == 1
```

## Fixtures

```python
import pytest

@pytest.fixture
def sample_data():
    return {"name": "Alice", "age": 30}

def test_user(sample_data):
    assert sample_data["name"] == "Alice"
```

## Setup and Teardown

```python
@pytest.fixture
def resource():
    # setup
    obj = SomeResource()
    yield obj
    # teardown
    obj.cleanup()
```

## Parametrization

```python
import pytest

@pytest.mark.parametrize("a,b,result", [
    (1, 2, 3),
    (4, 5, 9),
])
def test_add(a, b, result):
    assert a + b == result
```

## Expected Exceptions

```python
import pytest

def divide(x, y):
    return x / y

def test_zero_division():
    with pytest.raises(ZeroDivisionError):
        divide(1, 0)
```

## Skipping Tests

```python
import pytest

@pytest.mark.skip(reason="not implemented yet")
def test_feature():
    ...

@pytest.mark.skipif(sys.platform == "win32", reason="Windows not supported")
def test_only_on_unix():
    ...
```

## Custom Marks

```python
# pytest.ini
[pytest]
markers =
    slow: marks tests as slow
```

```python
import pytest

@pytest.mark.slow
def test_big_job():
    ...
```

Run with custom mark:

```bash
pytest -m slow
```

## Capturing Output

```python
def test_stdout(capsys):
    print("hello")
    captured = capsys.readouterr()
    assert "hello" in captured.out
```

## Temporary Files and Directories

```python
def test_tmp_path(tmp_path):
    file = tmp_path / "file.txt"
    file.write_text("hello")
    assert file.read_text() == "hello"
```
