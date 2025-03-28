# Celery Cheat Sheet (Python Task Queue)

## Installation

```bash
pip install celery
```

For Redis broker:

```bash
pip install redis
```

## Create a Celery App

```python
# tasks.py
from celery import Celery

app = Celery("tasks", broker="redis://localhost:6379/0")

@app.task
def add(x, y):
    return x + y
```

## Run a Worker

```bash
celery -A tasks worker --loglevel=info
```

## Call Tasks

```python
from tasks import add

add.delay(4, 6)     # Async call
result = add.apply_async((4, 6))
result.get()        # Wait for result
```

## Check Status

```python
result.ready()   # True if done
result.successful()
result.result
```

## Configure Backend

```python
# tasks.py
app = Celery("tasks",
    broker="redis://localhost:6379/0",
    backend="redis://localhost:6379/0"
)
```

## Retry on Failure

```python
@app.task(bind=True, max_retries=3)
def fragile_task(self):
    try:
        do_something()
    except Exception as e:
        raise self.retry(exc=e, countdown=5)
```

## Set Task Options

```python
@app.task(name="my_task", rate_limit="10/m", time_limit=30)
def my_task():
    ...
```

## Periodic Tasks (Celery Beat)

Install:

```bash
pip install celery[redis] django-celery-beat
```

Add to your app:

```python
from celery.schedules import crontab

app.conf.beat_schedule = {
    "say-hello-every-minute": {
        "task": "say_hello",
        "schedule": crontab(minute="*/1"),
    },
}
```

Start beat:

```bash
celery -A tasks beat --loglevel=info
```

## Chaining Tasks

```python
from celery import chain

chain(add.s(2, 2), add.s(4))().get()
```

## Groups

```python
from celery import group

job = group(add.s(i, i) for i in range(5))()
job.get()
```

## Chords (Group + Callback)

```python
from celery import chord

chord(group(add.s(i, i) for i in range(5)))(add.s(100)).get()
```

## Task Annotations

```python
app.conf.task_annotations = {
    'tasks.add': {'rate_limit': '10/s'}
}
```

## Error Handling

```python
@app.task(autoretry_for=(Exception,), retry_kwargs={'max_retries': 3})
def error_prone():
    ...
```

## Logging

```python
import logging

logger = logging.getLogger(__name__)

@app.task
def log_message():
    logger.info("Task is running")
```

## Task States

- `PENDING`
- `STARTED`
- `SUCCESS`
- `FAILURE`
- `RETRY`
- `REVOKED`

## Inspect Workers

```bash
celery -A tasks status
celery -A tasks inspect active
celery -A tasks inspect scheduled
```

## Revoke Task

```python
result.revoke(terminate=True)
```

## Graceful Shutdown

```bash
pkill -TERM -f 'celery worker'
```
