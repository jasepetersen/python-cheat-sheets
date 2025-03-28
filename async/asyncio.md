# Python asyncio Cheat Sheet

## Import and Event Loop

```python
import asyncio

async def main():
    print("Hello")
    await asyncio.sleep(1)
    print("World")

asyncio.run(main())
```

## Coroutines

```python
async def say_hello():
    await asyncio.sleep(1)
    return "Hello"
```

## Running Coroutines

```python
result = asyncio.run(say_hello())
```

## await and sleep

```python
await asyncio.sleep(2)
```

## Creating Tasks

```python
async def foo():
    await asyncio.sleep(1)
    return "foo"

async def bar():
    await asyncio.sleep(2)
    return "bar"

async def main():
    task1 = asyncio.create_task(foo())
    task2 = asyncio.create_task(bar())
    result1 = await task1
    result2 = await task2
```

## asyncio.gather

```python
results = await asyncio.gather(
    foo(),
    bar()
)
```

## asyncio.wait

```python
done, pending = await asyncio.wait([
    foo(),
    bar()
])
```

## asyncio.as_completed

```python
for coro in asyncio.as_completed([foo(), bar()]):
    result = await coro
```

## asyncio.Timeout

```python
try:
    await asyncio.wait_for(foo(), timeout=1)
except asyncio.TimeoutError:
    print("Timed out")
```

## Queues

```python
queue = asyncio.Queue()

await queue.put("item")
item = await queue.get()
```

## Event

```python
event = asyncio.Event()

async def waiter():
    await event.wait()
    print("Event triggered!")

event.set()  # triggers event
```

## Semaphore

```python
semaphore = asyncio.Semaphore(3)

async def limited_task():
    async with semaphore:
        await asyncio.sleep(1)
```

## Lock

```python
lock = asyncio.Lock()

async def safe_task():
    async with lock:
        print("Only one at a time")
```

## Running Code in Threads

```python
import time

def blocking_io():
    time.sleep(2)
    return "done"

result = await asyncio.to_thread(blocking_io)
```

## Subprocess

```python
proc = await asyncio.create_subprocess_exec(
    "ls", "-l",
    stdout=asyncio.subprocess.PIPE,
    stderr=asyncio.subprocess.PIPE
)

stdout, stderr = await proc.communicate()
```

## Exception Handling

```python
try:
    await some_task()
except Exception as e:
    print(f"Error: {e}")
```

## Canceling Tasks

```python
task = asyncio.create_task(some_task())
task.cancel()

try:
    await task
except asyncio.CancelledError:
    print("Task was cancelled")
```

## Debug Mode

```python
import asyncio
asyncio.run(main(), debug=True)
```

## Notes

- `await` only works inside `async def`
- `asyncio.run()` is the recommended entry point (Python 3.7+)
- Use `create_task` to run coroutines concurrently
