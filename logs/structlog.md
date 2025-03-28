# structlog Cheat Sheet

## Installation

```bash
pip install structlog
```

## Basic Setup

```python
import logging
import structlog

logging.basicConfig(format="%(message)s", level=logging.INFO)

structlog.configure(
    wrapper_class=structlog.make_filtering_bound_logger(logging.INFO),
    processors=[
        structlog.processors.add_log_level,
        structlog.processors.TimeStamper(fmt="iso"),
        structlog.processors.JSONRenderer()
    ]
)

log = structlog.get_logger()
log.info("hello", user="alice", action="login")
```

## Bind Context

```python
log = structlog.get_logger().bind(user="alice")
log.info("logged_in")
```

## Unbind Context

```python
log = log.unbind("user")
log.info("logged_out")
```

## Rebind Context

```python
log = log.bind(user="bob")
log.info("changed_user")
```

## Adding Processors

```python
structlog.configure(
    processors=[
        structlog.processors.TimeStamper(fmt="iso"),
        structlog.stdlib.add_log_level,
        structlog.processors.StackInfoRenderer(),
        structlog.processors.format_exc_info,
        structlog.processors.JSONRenderer()
    ]
)
```

## Logging Exceptions

```python
try:
    1 / 0
except ZeroDivisionError:
    log.exception("divide_by_zero")
```

## Custom Logger Format (Key-Value Text)

```python
import structlog

structlog.configure(
    processors=[
        structlog.processors.KeyValueRenderer(key_order=["event", "user"]),
    ]
)

log = structlog.get_logger()
log.info("login", user="alice")
```

## Use with Standard Logging

```python
import structlog

structlog.configure(
    wrapper_class=structlog.stdlib.BoundLogger,
    logger_factory=structlog.stdlib.LoggerFactory(),
    processors=[
        structlog.stdlib.add_log_level,
        structlog.stdlib.PositionalArgumentsFormatter(),
        structlog.processors.StackInfoRenderer(),
        structlog.processors.format_exc_info,
        structlog.processors.TimeStamper(fmt="iso"),
        structlog.processors.JSONRenderer(),
    ]
)

log = structlog.get_logger()
log.info("hello", user="bob")
```

## Debugging Processor Chain

```python
structlog.configure(
    processors=[
        structlog.dev.set_exc_info,
        structlog.dev.ConsoleRenderer()
    ]
)
```

## Set Log Level Dynamically

```python
import logging

structlog.configure(
    wrapper_class=structlog.make_filtering_bound_logger(logging.DEBUG)
)
```
