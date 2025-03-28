# Requests Library Cheat Sheet

## Installation

```bash
pip install requests
```

## Basic GET Request

```python
import requests

response = requests.get("https://api.example.com")
print(response.status_code)
print(response.text)
```

## Query Parameters

```python
params = {"q": "python", "page": 2}
response = requests.get("https://api.example.com/search", params=params)
```

## POST Request with JSON

```python
data = {"name": "Alice", "age": 30}
response = requests.post("https://api.example.com/users", json=data)
```

## POST Request with Form Data

```python
data = {"username": "alice", "password": "secret"}
response = requests.post("https://api.example.com/login", data=data)
```

## Custom Headers

```python
headers = {"Authorization": "Bearer TOKEN"}
response = requests.get("https://api.example.com/protected", headers=headers)
```

## Handling JSON Response

```python
data = response.json()
print(data["name"])
```

## File Upload

```python
files = {"file": open("example.txt", "rb")}
response = requests.post("https://api.example.com/upload", files=files)
```

## Timeout

```python
response = requests.get("https://api.example.com", timeout=5)
```

## Error Handling

```python
try:
    response = requests.get("https://api.example.com", timeout=5)
    response.raise_for_status()
except requests.exceptions.RequestException as e:
    print(f"Error: {e}")
```

## Sessions (Persistent Connections)

```python
session = requests.Session()
session.headers.update({"User-Agent": "my-app"})

response = session.get("https://api.example.com")
```

## Redirects

```python
response = requests.get("https://example.com", allow_redirects=True)
```

## Download Binary File

```python
response = requests.get("https://example.com/image.png")
with open("image.png", "wb") as f:
    f.write(response.content)
```

## HTTP Methods

```python
requests.get(url)
requests.post(url, data={})
requests.put(url, data={})
requests.patch(url, data={})
requests.delete(url)
```
