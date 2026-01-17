# wsgiref Module

The `wsgiref` module provides reference implementations and utilities for WSGI (Web Server Gateway Interface) servers and applications.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Server setup | O(1) | O(1) | Create server |
| Handle request | O(n) | O(n) | n = request size |

## WSGI Server Implementation

### Simple WSGI Application

```python
from wsgiref.simple_server import make_server

def application(environ, start_response):
    """WSGI application - O(1)"""
    path = environ.get('PATH_INFO', '')
    
    if path == '/':
        response_body = b'Hello, World!'
        status = '200 OK'
    else:
        response_body = b'Not Found'
        status = '404 Not Found'
    
    response_headers = [
        ('Content-Type', 'text/plain'),
        ('Content-Length', str(len(response_body)))
    ]
    start_response(status, response_headers)
    return [response_body]

# Create server - O(1)
httpd = make_server('localhost', 8000, application)

# Serve - O(m)
print("Serving at http://localhost:8000")
httpd.serve_forever()
```

## Related Documentation

- [http.server Module](http.md)
- [urllib Module](urllib.md)
