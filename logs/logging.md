# Python Logging Cheat Sheet

## Import and Basic Config

```python
import logging

logging.basicConfig(level=logging.INFO)
logging.info("This is an info message")
```

## Logging Levels

```python
logging.debug("Debug details")     # Lowest level
logging.info("General info")       # Default level
logging.warning("Something's wrong")
logging.error("An error occurred")
logging.critical("Severe error")
```

## Set Level

```python
logging.basicConfig(level=logging.DEBUG)
```

## Custom Format

```python
logging.basicConfig(
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s"
)
```

## Log to a File

```python
logging.basicConfig(
    filename="app.log",
    filemode="a",  # or "w" to overwrite
    level=logging.INFO,
    format="%(asctime)s - %(levelname)s - %(message)s"
)
```

## Named Logger

```python
logger = logging.getLogger("myapp")
logger.setLevel(logging.DEBUG)

logger.info("Logger with a name")
```

## Adding a Handler

```python
handler = logging.FileHandler("output.log")
handler.setLevel(logging.WARNING)

formatter = logging.Formatter("%(name)s - %(levelname)s - %(message)s")
handler.setFormatter(formatter)

logger = logging.getLogger("custom")
logger.addHandler(handler)

logger.warning("This will go to output.log")
```

## Disable Propagation

```python
logger.propagate = False
```

## Exception Logging

```python
try:
    1 / 0
except Exception as e:
    logging.exception("An exception occurred")
```

## Logging from Multiple Files

```python
# In each module:
import logging

logger = logging.getLogger(__name__)
logger.setLevel(logging.INFO)
```

## Reset Logging (for Jupyter or reconfiguring)

```python
import logging
for handler in logging.root.handlers[:]:
    logging.root.removeHandler(handler)
```
