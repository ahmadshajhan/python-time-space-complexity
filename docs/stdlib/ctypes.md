# Ctypes Module

The `ctypes` module provides C-compatible data types and allows calling functions in DLLs (Windows) or shared libraries (Unix).

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `CDLL(name)` | O(1) | O(1) | Load library |
| `c_int/c_float/c_char` | O(1) | O(1) | Create type |
| `function_call()` | O(n) | O(n) | n = arg count |
| `Structure/Union` | O(1) | O(1) | Define class |
| `sizeof(obj)` | O(1) | O(1) | Size of ctypes type/instance |
| `addressof(obj)` | O(1) | O(1) | Address of ctypes instance |
| `byref(obj)` | O(1) | O(1) | Pass by reference helper |
| `pointer(obj)` | O(1) | O(1) | Create pointer to instance |
| `cast(obj, type)` | O(1) | O(1) | Pointer cast |
| `create_string_buffer(n)` | O(n) | O(n) | Allocate byte buffer |
| `create_unicode_buffer(n)` | O(n) | O(n) | Allocate wchar buffer |
| `memmove` / `memset` | O(n) | O(1) | n = bytes moved/filled |
| `string_at` / `wstring_at` | O(n) | O(n) | n = bytes/characters read |
| `get_errno` / `set_errno` | O(1) | O(1) | Thread-local errno |
| Scalar types (e.g., `c_int`, `c_double`) | O(1) | O(1) | Type constructors |
| Fixed-width ints (e.g., `c_int32`, `c_uint64`) | O(1) | O(1) | Type constructors |
| Pointers/arrays (`POINTER`, `ARRAY`) | O(1) | O(1) | Type constructors |
| Structs/unions (`Structure`, `Union`) | O(1) | O(1) | Type constructors |
| Endian variants (`LittleEndian*`, `BigEndian*`) | O(1) | O(1) | Type constructors |
| Callables (`CFUNCTYPE`, `PYFUNCTYPE`) | O(1) | O(1) | Function type factories |
| Library loaders (`cdll`, `pydll`, `pythonapi`) | O(1) | O(1) | Loader singletons |

## Common Operations

### Loading and Calling C Functions

```python
from ctypes import CDLL, c_int, c_double

# O(1) - load standard C library
import ctypes
libc = ctypes.CDLL(None)  # Unix
# or on Windows:
# msvcrt = ctypes.CDLL('msvcrt')

# O(1) - get function reference
sqrt = libc.sqrt

# O(1) - call C function with conversion
result = sqrt(16.0)  # Returns 4.0
print(result)

# With explicit types - O(1) for arg conversion
from ctypes import c_double, CDLL
libc = CDLL('libc.so.6')  # On Linux
sqrt = libc.sqrt
sqrt.argtypes = [c_double]  # O(1)
sqrt.restype = c_double     # O(1)
result = sqrt(16.0)         # O(1) typed call
```

### Working with C Data Types

```python
from ctypes import (
    c_int, c_float, c_char, c_bool,
    c_int32, c_int64, c_uint8
)

# O(1) - create instances
x = c_int(42)           # 32-bit integer
y = c_float(3.14)       # Float
z = c_char(b'A')        # Single char
flag = c_bool(True)     # Boolean

# O(1) - access values
print(x.value)          # 42
print(y.value)          # 3.14

# O(1) - modify values
x.value = 100
```

## Common Use Cases

### Calling System Functions

```python
from ctypes import CDLL, c_char_p, c_int
import ctypes

# Unix/Linux example
libc = ctypes.CDLL('libc.so.6')

# O(1) - strlen function
strlen = libc.strlen
strlen.argtypes = [c_char_p]
strlen.restype = c_int

# O(n) where n = string length (C-side)
text = b"Hello"
length = strlen(text)  # O(n)
print(length)  # 5
```

### Creating Structures

```python
from ctypes import Structure, c_int, c_char_p

# O(1) - define C struct equivalent
class Point(Structure):
    _fields_ = [
        ('x', c_int),
        ('y', c_int),
    ]

# O(1) - create instance
p = Point()
p.x = 10  # O(1)
p.y = 20  # O(1)

print(f"Point: ({p.x}, {p.y})")  # O(1)

# O(1) - construct with values
p2 = Point(x=5, y=15)
```

### Passing Structures to C Functions

```python
from ctypes import Structure, c_int, CDLL
import ctypes

class Point(Structure):
    _fields_ = [('x', c_int), ('y', c_int)]

# Assuming C function exists: int distance(Point p);
libc = ctypes.CDLL(None)
distance = libc.distance
distance.argtypes = [Point]  # O(1)
distance.restype = c_int     # O(1)

# O(1) - pass structure
p = Point(x=3, y=4)
dist = distance(p)  # O(1) + C computation
```

### Working with Pointers

```python
from ctypes import c_int, POINTER, pointer

# O(1) - create integer
x = c_int(42)

# O(1) - get pointer
ptr = pointer(x)

# O(1) - dereference pointer
print(ptr.contents.value)  # 42

# O(1) - modify through pointer
ptr.contents.value = 100
print(x.value)  # 100
```

### Arrays in Ctypes

```python
from ctypes import c_int, ARRAY

# O(1) - define array type
IntArray = c_int * 5

# O(n) - create array where n = size
arr = IntArray()

# O(1) - set values
arr[0] = 10
arr[1] = 20

# O(1) - get values
print(arr[0])  # 10

# O(n) - iterate all elements
for i in range(5):
    print(arr[i])
```

## Performance Tips

### Cache Library Loading

```python
from ctypes import CDLL

class LibraryCache:
    """Cache loaded libraries - O(1) access"""
    
    def __init__(self):
        self._libs = {}
    
    def get_lib(self, name):
        """O(1) cached or O(1) load"""
        if name not in self._libs:
            # O(1) to load DLL/SO
            self._libs[name] = CDLL(name)
        return self._libs[name]

# Usage
cache = LibraryCache()
libc = cache.get_lib('libc.so.6')  # O(1)
libc = cache.get_lib('libc.so.6')  # O(1) - cached
```

### Set argtypes Once

```python
from ctypes import CDLL, c_int, c_double
import ctypes

# Bad: Set argtypes each call (expensive)
libc = ctypes.CDLL('libc.so.6')
pow_func = libc.pow

for i in range(1000):
    pow_func.argtypes = [c_double, c_double]  # O(k) each time
    pow_func.restype = c_double
    result = pow_func(2.0, i)  # O(1)

# Good: Set once - O(k) + O(n) instead of O(n*k)
pow_func = libc.pow
pow_func.argtypes = [c_double, c_double]  # O(k) once
pow_func.restype = c_double

for i in range(1000):
    result = pow_func(2.0, i)  # O(1)
```

### Use by_reference for Large Structures

```python
from ctypes import Structure, c_int, CDLL, byref
import ctypes

class LargeStruct(Structure):
    _fields_ = [('data', c_int * 1000)]

# Bad: Pass by value (copies) - O(n)
func = ctypes.CDLL('libfoo').process
func.argtypes = [LargeStruct]
result = func(large_obj)  # O(n) copy

# Good: Pass by reference - O(1)
func.argtypes = [POINTER(LargeStruct)]
result = func(byref(large_obj))  # O(1) reference
```

## Version Notes

- **Python 2.5+**: ctypes available
- **Python 3.x**: All features available
- **Windows/Unix**: Portable across platforms
- **Python 3.11+**: Some optimizations

## Related Documentation

- [Subprocess Module](subprocess.md) - Alternative for external programs
- [Sys Module](sys.md) - Platform information
