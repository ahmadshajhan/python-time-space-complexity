# copyreg Module

The `copyreg` module provides a way to define pickle support for custom types, handling serialization of non-standard objects.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `pickle()` | O(1) | O(1) | Register pickler |
| `constructor()` | O(1) | O(1) | Register unpickler |
| `add_extension()` | O(1) | O(1) | Register extension code |
| `remove_extension()` | O(1) | O(1) | Remove extension code |
| `clear_extension_cache()` | O(n) | O(1) | n = cached entries |
| `dispatch_table` | O(1) | O(1) | Pickle dispatch registry |
| `pickle_complex()` | O(1) | O(1) | Built-in complex pickler |
| `pickle_super()` | O(1) | O(1) | Built-in super pickler |
| `pickle_union()` | O(1) | O(1) | Built-in union pickler |

## Custom Pickle Support

### Registering Custom Types

```python
import copyreg
import pickle

class MyClass:
    def __init__(self, value):
        self.value = value

# Register pickle functions - O(1)
def pickle_myclass(obj):
    return (unpickle_myclass, (obj.value,))

def unpickle_myclass(value):
    return MyClass(value)

copyreg.pickle(MyClass, pickle_myclass)

# Now can pickle - O(n)
obj = MyClass(42)
data = pickle.dumps(obj)

# Unpickle - O(n)
restored = pickle.loads(data)
print(restored.value)  # 42
```

## Related Documentation

- [pickle Module](pickle.md)
- [copy Module](copy.md)
