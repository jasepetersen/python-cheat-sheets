# PyMongo

## Installation

```bash
pip install pymongo
```

## Connect to MongoDB

```python
from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017")
db = client["mydatabase"]
collection = db["users"]
```

## Insert Documents

```python
# Single document
collection.insert_one({"name": "Alice", "age": 30})

# Multiple documents
collection.insert_many([
    {"name": "Bob", "age": 25},
    {"name": "Carol", "age": 40}
])
```

## Find Documents

```python
# First match
user = collection.find_one({"name": "Alice"})

# All matches
users = collection.find({"age": {"$gt": 25}})
for user in users:
    print(user)
```

## Update Documents

```python
# Single document
collection.update_one(
    {"name": "Alice"},
    {"$set": {"age": 31}}
)

# Multiple documents
collection.update_many(
    {"age": {"$lt": 30}},
    {"$inc": {"age": 1}}
)
```

## Delete Documents

```python
# Single document
collection.delete_one({"name": "Bob"})

# Multiple documents
collection.delete_many({"age": {"$gte": 40}})
```

## Query Operators

```python
# $gt, $lt, $eq, $ne, $in, $nin, $exists, etc.
collection.find({"age": {"$gt": 25}})
collection.find({"name": {"$in": ["Alice", "Carol"]}})
```

## Sorting, Limiting, Skipping

```python
collection.find().sort("age", -1).limit(5).skip(2)
```

## Indexes

```python
collection.create_index("name")
```

## Aggregation Pipeline

```python
pipeline = [
    {"$match": {"age": {"$gte": 30}}},
    {"$group": {"_id": "$name", "total": {"$sum": 1}}}
]
results = collection.aggregate(pipeline)
```

## Counting Documents

```python
count = collection.count_documents({"age": {"$gt": 25}})
```

## Drop Collection or Database

```python
collection.drop()
client.drop_database("mydatabase")
```

## ObjectId

```python
from bson import ObjectId

_id = ObjectId("507f1f77bcf86cd799439011")
doc = collection.find_one({"_id": _id})
```
