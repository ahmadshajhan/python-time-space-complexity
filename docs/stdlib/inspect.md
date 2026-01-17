# Inspect Module Complexity

The `inspect` module provides utilities for inspecting live objects, including modules, classes, methods, functions, and code objects.

## Common Operations

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `getmembers(obj)` | O(m) | O(m) | Get all members of object |
| `getdoc(obj)` | O(1) | O(n) | Get docstring |
| `signature(func)` | O(p) | O(p) | Get function signature |
| `getsource(obj)` | O(n) | O(n) | Get source code |
| `getsourcelines(obj)` | O(n) | O(n) | Get source + line numbers |
| `getfile(obj)` | O(1) | O(1) | Get file path |
| `isfunction(obj)` | O(1) | O(1) | Check if function |
| `ismethod(obj)` | O(1) | O(1) | Check if method |
| `isclass(obj)` | O(1) | O(1) | Check if class |

## Object Introspection

### getmembers()

#### Time Complexity: O(m)

Where m = number of members.

```python
import inspect

# Get all members: O(m) where m = attributes + methods
members = inspect.getmembers(obj)  # O(m)

# Get members matching predicate: O(m) to scan all
functions = inspect.getmembers(obj, inspect.isfunction)  # O(m)

# Get attributes only
for name, value in members:
    print(f'{name}: {type(value)}')
```

#### Space Complexity: O(m)

```python
import inspect

# List of all members stored
members = inspect.getmembers(obj)  # O(m) space
```

### Type Checking

#### Time Complexity: O(1)

```python
import inspect

def check_type(obj):
    # O(1) checks
    if inspect.isfunction(obj):
        return 'function'
    elif inspect.ismethod(obj):
        return 'method'
    elif inspect.isclass(obj):
        return 'class'
    elif inspect.ismodule(obj):
        return 'module'
    elif inspect.isbuiltin(obj):
        return 'builtin'
    return 'other'

result = check_type(func)  # O(1)
```

#### Space Complexity: O(1)

```python
import inspect

is_func = inspect.isfunction(obj)  # O(1) space
```

## Function Signatures

### signature()

#### Time Complexity: O(p)

Where p = number of parameters.

```python
import inspect

# Get signature: O(p) to analyze parameters
sig = inspect.signature(func)  # O(p)

# Access parameters: O(1)
for param_name, param in sig.parameters.items():
    print(f'{param_name}: {param.annotation}')  # O(p) total

# Get return annotation: O(1)
return_type = sig.return_annotation
```

#### Space Complexity: O(p)

```python
import inspect

sig = inspect.signature(func)  # O(p) space for parameters
```

## Source Code Retrieval

### getsource()

#### Time Complexity: O(n)

Where n = source code size.

```python
import inspect

# Get source: O(n) to read file
source = inspect.getsource(func)  # O(n)

# Get lines with line numbers: O(n)
source_lines, start_line = inspect.getsourcelines(func)  # O(n)

# Source is read from disk and cached
# Subsequent calls may be O(1) from cache
```

#### Space Complexity: O(n)

```python
import inspect

# Entire source code stored
source = inspect.getsource(obj)  # O(n) space
```

## Stack and Frame Inspection

### Stack Frames

#### Time Complexity: O(d)

Where d = call stack depth.

```python
import inspect

# Get current frame: O(1)
frame = inspect.currentframe()  # O(1)

# Get call stack: O(d) where d = depth
stack = inspect.stack()  # O(d)

# Get traceback: O(d)
traceback = inspect.trace()  # O(d)

# Process stack: O(d)
for frame_info in stack:
    filename = frame_info.filename
    line_number = frame_info.lineno
```

#### Space Complexity: O(d)

```python
import inspect

# Stack stored in memory
stack = inspect.stack()  # O(d) space
```

## Common Patterns

### Find All Functions in Module

```python
import inspect

def get_functions(module):
    """Get all functions in module: O(m)"""
    return inspect.getmembers(module, inspect.isfunction)  # O(m)

funcs = get_functions(my_module)  # O(m) where m = functions
```

### Get Function Parameter Info

```python
import inspect

def analyze_function(func):
    """Analyze function parameters: O(p)"""
    sig = inspect.signature(func)  # O(p)
    
    for param_name, param in sig.parameters.items():  # O(p)
        print(f'{param_name}: {param.annotation}')
    
    return sig.return_annotation

analyze_function(my_func)  # O(p) where p = parameters
```

### Debug Call Stack

```python
import inspect

def debug_caller():
    """Get info about caller: O(d)"""
    stack = inspect.stack()  # O(d)
    caller_frame = stack[1]  # Direct access O(1)
    
    return {
        'function': caller_frame.function,
        'filename': caller_frame.filename,
        'line': caller_frame.lineno,
    }

info = debug_caller()  # O(d) where d = stack depth
```

### Introspect Class Hierarchy

```python
import inspect

def show_mro(cls):
    """Show method resolution order: O(c)"""
    mro = inspect.getmro(cls)  # O(c) to get class hierarchy
    for base in mro:
        print(base.__name__)
    return mro

mro = show_mro(MyClass)  # O(c) where c = classes in hierarchy
```

## Performance Characteristics

### Best Practices

```python
import inspect

# Good: Cache signatures
sig = inspect.signature(func)  # O(p) once
for _ in range(1000):
    # Reuse cached signature
    params = sig.parameters  # O(1)

# Good: Use specific checks
if inspect.isfunction(obj):  # O(1)
    process_function(obj)

# Avoid: getmembers() on large objects
members = inspect.getmembers(huge_module)  # O(m) - slow!

# Better: Use filtered getmembers
funcs = inspect.getmembers(module, inspect.isfunction)  # O(m)
```

### Stack Inspection Overhead

```python
import inspect

# Stack inspection is expensive
def expensive_debug():
    stack = inspect.stack()  # O(d) where d = deep call stack
    # Each frame requires system calls

# Better: Cache if inspecting repeatedly
import functools
frame_cache = None

def get_caller_info():
    global frame_cache
    if frame_cache is None:
        stack = inspect.stack()  # O(d) once
        frame_cache = stack[1]
    return frame_cache
```

## Comparison with Alternatives

```python
import inspect
import sys

# inspect (high-level, slower)
sig = inspect.signature(func)  # O(p)

# __code__ object (low-level, faster)
code = func.__code__
arg_count = code.co_argcount  # O(1)

# sys._getframe (faster than stack())
frame = sys._getframe(0)  # O(1) vs O(d)
```

## Version Notes

- **Python 3.3+**: `signature()` added
- **Python 3.5+**: Improvements to signature handling
- **Python 3.10+**: Parameter behavior changes

## Related Documentation

- [Dis Module](dis.md) - Bytecode disassembly
- [Traceback Module](traceback.md) - Exception handling
- [Types Module](types.md) - Type objects
