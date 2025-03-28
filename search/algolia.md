# Algolia Python Cheat Sheet

## Installation

```bash
pip install algoliasearch
```

## Initialize Client

```python
from algoliasearch.search_client import SearchClient

client = SearchClient.create("YourApplicationID", "YourAdminAPIKey")
index = client.init_index("your_index_name")
```

## Add / Replace Objects

```python
# Single object
index.save_object({
    "objectID": "1",
    "name": "Alice"
})

# Multiple objects
index.save_objects([
    {"objectID": "1", "name": "Alice"},
    {"objectID": "2", "name": "Bob"}
])
```

## Partial Update

```python
index.partial_update_object({
    "objectID": "1",
    "age": 30
})
```

## Delete Objects

```python
index.delete_object("1")

index.delete_objects(["1", "2"])
```

## Search

```python
results = index.search("Alice")
for hit in results["hits"]:
    print(hit["name"])
```

## Set Settings

```python
index.set_settings({
    "searchableAttributes": ["name", "email"],
    "customRanking": ["desc(score)"]
})
```

## Browse Index

```python
for hit in index.browse_objects():
    print(hit)
```

## Clear Index

```python
index.clear_objects()
```

## Get Object

```python
user = index.get_object("1")
```

## Batch Operations

```python
index.batch([
    {"action": "addObject", "body": {"objectID": "1", "name": "Alice"}},
    {"action": "deleteObject", "body": {"objectID": "2"}}
])
```

## Wait for Operations

```python
res = index.save_object({"objectID": "1", "name": "Alice"})
res.wait()
```

## Faceted Search

```python
index.set_settings({
    "attributesForFaceting": ["searchable(category)"]
})

results = index.search("jeans", {
    "facets": ["category"]
})
```

## Geo Search

```python
index.set_settings({
    "searchableAttributes": ["name"],
    "attributesForFaceting": ["_geoloc"]
})

results = index.search("", {
    "aroundLatLng": "48.8566,2.3522",  # Paris
    "aroundRadius": 10000              # in meters
})
```

## Synonyms

```python
index.save_synonym("red-color", {
    "objectID": "red-color",
    "type": "synonym",
    "synonyms": ["red", "crimson", "scarlet"]
})
```

## Rules

```python
index.save_rule("hide-expired", {
    "objectID": "hide-expired",
    "condition": {
        "pattern": "expired",
        "anchoring": "is"
    },
    "consequence": {
        "filterPromotes": False,
        "filters": "isExpired != true"
    }
})
```

## Analytics (Optional)

- Use Algolia Dashboard or REST API for click & conversion analytics.
