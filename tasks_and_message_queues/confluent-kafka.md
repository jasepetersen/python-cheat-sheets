# confluent-kafka Cheat Sheet

## Installation

```bash
pip install confluent-kafka
```

## Basic Producer

```python
from confluent_kafka import Producer

conf = {'bootstrap.servers': 'localhost:9092'}
producer = Producer(conf)

def delivery_report(err, msg):
    if err is not None:
        print('Delivery failed:', err)
    else:
        print(f'Message delivered to {msg.topic()} [{msg.partition()}]')

producer.produce('my-topic', key='key1', value='hello world', callback=delivery_report)
producer.flush()
```

## Basic Consumer

```python
from confluent_kafka import Consumer

conf = {
    'bootstrap.servers': 'localhost:9092',
    'group.id': 'my-group',
    'auto.offset.reset': 'earliest'
}

consumer = Consumer(conf)
consumer.subscribe(['my-topic'])

try:
    while True:
        msg = consumer.poll(1.0)
        if msg is None:
            continue
        if msg.error():
            print("Consumer error:", msg.error())
            continue

        print(f"Received: {msg.value().decode('utf-8')}")

except KeyboardInterrupt:
    pass
finally:
    consumer.close()
```

## Produce JSON

```python
import json

data = {'user': 'alice', 'action': 'login'}
producer.produce('json-topic', value=json.dumps(data))
producer.flush()
```

## Consume JSON

```python
msg = consumer.poll(1.0)
if msg:
    data = json.loads(msg.value())
    print(data['user'])
```

## Keyed Messages

```python
producer.produce('my-topic', key='user-id-1', value='action')
```

## Kafka Configuration Options

**Producer Options:**

- `bootstrap.servers`: Kafka broker address
- `queue.buffering.max.messages`
- `queue.buffering.max.ms`

**Consumer Options:**

- `group.id`: consumer group ID
- `auto.offset.reset`: earliest / latest
- `enable.auto.commit`: true/false

## Manual Offset Commit

```python
consumer.commit()
```

## Consuming from Specific Partition

```python
from confluent_kafka import TopicPartition

partition = TopicPartition('my-topic', 0)
consumer.assign([partition])
```

## High-Level Features

- Kafka guarantees message ordering within a partition
- Consumers in a group divide partitions among themselves
- Kafka retains messages even after consumption (based on retention policy)
- `confluent-kafka` is a performant C-based client for Kafka

## Alternatives

You can also use:

```bash
pip install kafka-python
```

But `confluent-kafka` is preferred for production use due to performance and stability.
