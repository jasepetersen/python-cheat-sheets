# Gevent Cheat Sheet (Greenlets & Asynchronous IO)

## Installation

```bash
pip install gevent
```

## Monkey Patching (Patch Standard Library)

```python
from gevent import monkey
monkey.patch_all()
```

Patch early (before any standard lib imports):

```python
import gevent.monkey
gevent.monkey.patch_all()

import requests  # now runs asynchronously with gevent
```

## Greenlets (Lightweight Coroutines)

```python
import gevent

def task(name):
    print(f"{name} started")
    gevent.sleep(1)
    print(f"{name} done")

g1 = gevent.spawn(task, "A")
g2 = gevent.spawn(task, "B")

gevent.joinall([g1, g2])
```

## Sleep

```python
gevent.sleep(seconds)
```

## Using Greenlet Directly

```python
from gevent import Greenlet

def run(x, y):
    print(x + y)

g = Greenlet(run, 1, 2)
g.start()
g.join()
```

## Asynchronous Networking (gevent-socket)

```python
import gevent
import socket

def get_host(host):
    print(f"Resolving {host}")
    print(socket.gethostbyname(host))

hosts = ['google.com', 'github.com', 'python.org']
jobs = [gevent.spawn(get_host, h) for h in hosts]
gevent.joinall(jobs)
```

## Timeout

```python
from gevent import Timeout

try:
    with Timeout(2):
        gevent.sleep(3)
except Timeout:
    print("Timed out!")
```

## Event Object (Coordination)

```python
from gevent.event import Event

evt = Event()

def waiter():
    print("Waiting...")
    evt.wait()
    print("Fired!")

gevent.spawn(waiter)
gevent.sleep(1)
evt.set()
```

## Queue

```python
from gevent.queue import Queue

q = Queue()

def producer():
    for i in range(3):
        q.put(i)

def consumer():
    while not q.empty():
        print(q.get())

gevent.joinall([
    gevent.spawn(producer),
    gevent.spawn(consumer)
])
```

## Pool

```python
from gevent.pool import Pool

pool = Pool(5)

def work(n):
    gevent.sleep(1)
    print(f"Task {n} done")

for i in range(10):
    pool.spawn(work, i)

pool.join()
```

## Server Example

```python
from gevent.pywsgi import WSGIServer

def app(env, start_response):
    start_response('200 OK', [('Content-Type', 'text/plain')])
    return [b"Hello from Gevent!\n"]

server = WSGIServer(('0.0.0.0', 8000), app)
server.serve_forever()
```

## Notes

- Gevent uses `libev` under the hood.
- Use `monkey.patch_all()` for cooperative IO across standard libraries.
- Great for IO-bound concurrency (not CPU-bound).
