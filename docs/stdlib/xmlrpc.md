# xmlrpc Module

The `xmlrpc` module provides tools for XML-RPC (Remote Procedure Call) clients and servers, encoding procedure calls in XML.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `ServerProxy()` | O(1) | O(1) | Create client |
| RPC call | O(n) | O(n) | n = request/response size |
| Server dispatch | O(1) | O(1) | Route to handler |

## XML-RPC Client and Server

### XML-RPC Client

```python
import xmlrpc.client

# Create proxy - O(1)
server = xmlrpc.client.ServerProxy('http://example.com/rpc')

# Call remote function - O(n)
result = server.add(3, 4)
print(result)  # 7

# Call with complex types - O(n)
data = {'name': 'Alice', 'age': 30}
result = server.process_data(data)
```

### XML-RPC Server

```python
import xmlrpc.server
import socketserver

class MyFunctions:
    def add(self, a, b):
        return a + b
    
    def multiply(self, a, b):
        return a * b

# Create server - O(1)
server = xmlrpc.server.SimpleXMLRPCServer(('localhost', 8000))

# Register functions - O(1) each
server.register_instance(MyFunctions())

# Serve - O(m)
server.serve_forever()
```

## Related Documentation

- [json Module](json.md)
- [socket Module](socket.md)
