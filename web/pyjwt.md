# PyJWT (JSON Web Token) Cheat Sheet

## Installation

```bash
pip install pyjwt
```

## Basic Usage

```python
import jwt

payload = {"user_id": 123}
secret = "mysecret"

token = jwt.encode(payload, secret, algorithm="HS256")
print(token)

decoded = jwt.decode(token, secret, algorithms=["HS256"])
print(decoded)
```

## Set Expiration

```python
import jwt
import datetime

payload = {
    "user_id": 123,
    "exp": datetime.datetime.utcnow() + datetime.timedelta(hours=1)
}

token = jwt.encode(payload, "mysecret", algorithm="HS256")
```

## Handle Expired Tokens

```python
import jwt
from jwt.exceptions import ExpiredSignatureError

try:
    decoded = jwt.decode(token, "mysecret", algorithms=["HS256"])
except ExpiredSignatureError:
    print("Token has expired")
```

## Custom Claims

```python
payload = {
    "user_id": 123,
    "role": "admin",
    "permissions": ["read", "write"]
}
```

## Decode Without Verification (Not Recommended)

```python
decoded = jwt.decode(token, options={"verify_signature": False})
```

## Supported Algorithms

- HS256 (default)
- HS384
- HS512
- RS256
- RS384
- RS512
- ES256
- ES384
- ES512
- PS256
- PS384
- PS512
- EdDSA

## RS256 Example

```python
private_key = open("private.pem").read()
public_key = open("public.pem").read()

token = jwt.encode(payload, private_key, algorithm="RS256")
decoded = jwt.decode(token, public_key, algorithms=["RS256"])
```

## Verify Signature

```python
jwt.decode(token, "mysecret", algorithms=["HS256"])
```

## JWT Parts

A JWT has 3 parts separated by dots:

```
header.payload.signature
```

Example:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9
.eyJ1c2VyX2lkIjoxMjN9
.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

- Header: algorithm and token type
- Payload: claims/data
- Signature: verifies data integrity
