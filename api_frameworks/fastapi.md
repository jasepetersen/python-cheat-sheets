# FastAPI Cheat Sheet

## Installation

```bash
pip install fastapi uvicorn
```

## Basic App

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}
```

## Run the Server

```bash
uvicorn main:app --reload
```

## Path Parameters

```python
@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id}
```

## Query Parameters

```python
@app.get("/search/")
def search(q: str = ""):
    return {"query": q}
```

## Request Body with Pydantic

```python
from pydantic import BaseModel

class Item(BaseModel):
    name: str
    price: float

@app.post("/items/")
def create_item(item: Item):
    return item
```

## Form Data

```python
from fastapi import Form

@app.post("/login/")
def login(username: str = Form(...), password: str = Form(...)):
    return {"username": username}
```

## File Upload

```python
from fastapi import File, UploadFile

@app.post("/upload/")
def upload(file: UploadFile = File(...)):
    return {"filename": file.filename}
```

## Response Model

```python
@app.post("/items/", response_model=Item)
def create_item(item: Item):
    return item
```

## Status Codes

```python
from fastapi import status

@app.post("/items/", status_code=status.HTTP_201_CREATED)
def create_item(item: Item):
    return item
```

## Dependencies

```python
from fastapi import Depends

def get_token(token: str):
    return token

@app.get("/users/")
def read_users(token: str = Depends(get_token)):
    return {"token": token}
```

## Middleware

```python
from fastapi import Request

@app.middleware("http")
async def log_requests(request: Request, call_next):
    response = await call_next(request)
    return response
```

## CORS

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)
```

## Background Tasks

```python
from fastapi import BackgroundTasks

def write_log(message: str):
    with open("log.txt", "a") as f:
        f.write(message)

@app.post("/log/")
def log_message(message: str, background_tasks: BackgroundTasks):
    background_tasks.add_task(write_log, message)
    return {"message": "Logged"}
```
