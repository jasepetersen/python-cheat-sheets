# Redis + Python Cheat Sheet

## Installation

```bash
pip install redis
```

## Connect to Redis

```python
import redis

r = redis.Redis(host="localhost", port=6379, db=0)
```

## Set and Get Keys

```python
r.set("name", "Alice")
name = r.get("name")  # b'Alice'
name = name.decode()  # 'Alice'
```

## Key Expiration

```python
r.setex("temp", 10, "value")  # Expires in 10 seconds
r.expire("name", 60)          # Set TTL of 60 seconds
```

## Delete Keys

```python
r.delete("name")
```

## Check Existence

```python
r.exists("name")  # Returns 1 if exists, 0 if not
```

## Increment / Decrement

```python
r.set("counter", 1)
r.incr("counter")
r.decr("counter")
```

## Lists

```python
r.rpush("queue", "task1", "task2")  # Push to right
r.lpush("queue", "task0")           # Push to left
r.lpop("queue")                     # Pop from left
r.rpop("queue")                     # Pop from right
r.lrange("queue", 0, -1)            # Get all items
```

## Sets

```python
r.sadd("tags", "python", "redis")
r.srem("tags", "redis")
r.smembers("tags")     # Returns set of members
r.sismember("tags", "python")
```

## Hashes

```python
r.hset("user:1", mapping={"name": "Alice", "age": "30"})
r.hget("user:1", "name")
r.hgetall("user:1")
r.hdel("user:1", "age")
```

## Sorted Sets

```python
r.zadd("leaderboard", {"alice": 100, "bob": 80})
r.zincrby("leaderboard", 20, "bob")
r.zrange("leaderboard", 0, -1, withscores=True)
r.zrevrange("leaderboard", 0, -1, withscores=True)
```

## Pub/Sub

**Publisher:**

```python
r.publish("news", "hello world")
```

**Subscriber:**

```python
pubsub = r.pubsub()
pubsub.subscribe("news")

for message in pubsub.listen():
    print(message)
```

## Pipelining

```python
pipe = r.pipeline()
pipe.set("a", 1)
pipe.incr("a")
pipe.execute()
```

## Transactions (MULTI/EXEC)

```python
with r.pipeline() as pipe:
    pipe.multi()
    pipe.set("x", 10)
    pipe.set("y", 20)
    pipe.execute()
```

## Connection Pool

```python
pool = redis.ConnectionPool(host="localhost", port=6379, db=0)
r = redis.Redis(connection_pool=pool)
```

## JSON with `redis.json` (if using RedisJSON module)

```bash
pip install redis[json]
```

```python
from redis.commands.json.path import Path

r.json().set("doc", Path.root_path(), {"name": "Alice", "age": 30})
r.json().get("doc", Path(".name"))
```

## Flushing Data (Careful!)

```python
r.flushdb()     # Clear current DB
r.flushall()    # Clear all DBs
```
