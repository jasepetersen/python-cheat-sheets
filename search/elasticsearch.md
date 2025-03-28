# Elasticsearch + Python Cheat Sheet (using `elasticsearch` client)

## Installation

```bash
pip install elasticsearch
```

## Connect to Elasticsearch

```python
from elasticsearch import Elasticsearch

es = Elasticsearch("http://localhost:9200")
```

## Check Connection

```python
es.ping()  # Returns True if connected
```

## Create/Index a Document

```python
doc = {"title": "Hello", "views": 10}
es.index(index="articles", id=1, document=doc)
```

## Get a Document

```python
res = es.get(index="articles", id=1)
print(res["_source"])
```

## Update a Document

```python
es.update(index="articles", id=1, doc={"views": 15})
```

## Delete a Document

```python
es.delete(index="articles", id=1)
```

## Search Documents

```python
res = es.search(index="articles", query={"match": {"title": "hello"}})
for hit in res["hits"]["hits"]:
    print(hit["_source"])
```

## Match Multiple Fields

```python
query = {
    "multi_match": {
        "query": "hello",
        "fields": ["title", "content"]
    }
}
es.search(index="articles", query=query)
```

## Bool Query

```python
query = {
    "bool": {
        "must": [{"match": {"title": "python"}}],
        "filter": [{"term": {"published": True}}]
    }
}
es.search(index="articles", query=query)
```

## Create Index with Mapping

```python
mapping = {
    "mappings": {
        "properties": {
            "title": {"type": "text"},
            "views": {"type": "integer"},
            "tags": {"type": "keyword"},
            "published_at": {"type": "date"}
        }
    }
}
es.indices.create(index="articles", body=mapping)
```

## Delete Index

```python
es.indices.delete(index="articles")
```

## Bulk Indexing

```python
from elasticsearch.helpers import bulk

docs = [
    {"_index": "articles", "_id": 1, "_source": {"title": "Post 1"}},
    {"_index": "articles", "_id": 2, "_source": {"title": "Post 2"}}
]

bulk(es, docs)
```

## Aggregations

```python
query = {
    "aggs": {
        "avg_views": {"avg": {"field": "views"}}
    }
}
res = es.search(index="articles", size=0, body=query)
print(res["aggregations"]["avg_views"]["value"])
```

## Highlighting

```python
query = {
    "query": {"match": {"content": "python"}},
    "highlight": {"fields": {"content": {}}}
}
res = es.search(index="articles", body=query)
```

## Sort & Pagination

```python
es.search(index="articles", from_=0, size=10, sort="views:desc")
```

## Refresh Index

```python
es.indices.refresh(index="articles")
```

## Notes

- Use `keyword` for exact match and `text` for full-text search.
- Queries can be passed using `body=` in ES <8 and `query=` in ES 8+.
- Bulk indexing is faster for large data loads.
