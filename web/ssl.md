# Python SSL Cheat Sheet

## Importing SSL Module

```python
import ssl
```

## Create Default SSL Context

```python
context = ssl.create_default_context()
```

## Verify HTTPS Connection

```python
import ssl
import urllib.request

url = "https://example.com"
context = ssl.create_default_context()

with urllib.request.urlopen(url, context=context) as response:
    html = response.read()
```

## Disable Certificate Verification (Not Recommended)

```python
import ssl

context = ssl._create_unverified_context()
```

## Secure Sockets with `socket` + SSL

```python
import socket
import ssl

hostname = 'example.com'
port = 443

context = ssl.create_default_context()

with socket.create_connection((hostname, port)) as sock:
    with context.wrap_socket(sock, server_hostname=hostname) as ssock:
        print(ssock.version())
```

## SSL Context Options

```python
context = ssl.SSLContext(ssl.PROTOCOL_TLS_CLIENT)
context.load_verify_locations('path/to/ca-bundle.crt')
context.load_cert_chain(certfile="client.crt", keyfile="client.key")
```

## Server Side Example

```python
import ssl
import socket

context = ssl.SSLContext(ssl.PROTOCOL_TLS_SERVER)
context.load_cert_chain(certfile="server.crt", keyfile="server.key")

with socket.socket(socket.AF_INET, socket.SOCK_STREAM, 0) as sock:
    sock.bind(("0.0.0.0", 8443))
    sock.listen(5)
    with context.wrap_socket(sock, server_side=True) as ssock:
        conn, addr = ssock.accept()
```

## Checking Certificate

```python
import ssl
import socket

def get_cert(host, port=443):
    context = ssl.create_default_context()
    with socket.create_connection((host, port)) as sock:
        with context.wrap_socket(sock, server_hostname=host) as ssock:
            cert = ssock.getpeercert()
            return cert

print(get_cert("example.com"))
```

## Useful Constants

```python
ssl.CERT_NONE
ssl.CERT_OPTIONAL
ssl.CERT_REQUIRED
```

## Check SSL/TLS Version

```python
print(ssl.OPENSSL_VERSION)
```

## Common Protocols

```python
ssl.PROTOCOL_TLS_CLIENT   # For client connections
ssl.PROTOCOL_TLS_SERVER   # For server connections
ssl.PROTOCOL_TLS          # Generic TLS
```

## Disable Older Protocols

```python
context.options |= ssl.OP_NO_TLSv1
context.options |= ssl.OP_NO_TLSv1_1
```
