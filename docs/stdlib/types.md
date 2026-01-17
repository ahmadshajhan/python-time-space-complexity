# Types Module Complexity

The `types` module provides standard names for all Python built-in types, useful for type checking and dynamic type creation.

## Common Operations

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Type checking | O(1) | O(1) | Check if type matches |
| `FunctionType()` | O(1) | O(1) | Create function |
| `SimpleNamespace()` | O(n) | O(n) | Create namespace |
| `MappingProxyType()` | O(1) | O(1) | Create read-only view of dict; no copy made |

## Type Constants

### Type Checking

#### Time Complexity: O(1)

```python
import types

# Check type: O(1)
def my_func():
    pass

if isinstance(my_func, types.FunctionType):
    print("It's a function")  # O(1)

# Type comparisons: O(1)
if type(obj) == types.ListType:  # Deprecated, use list
    pass

# Check callable: O(1)
if isinstance(obj, types.FunctionType):
    pass
```

#### Space Complexity: O(1)

```python
import types

is_func = isinstance(obj, types.FunctionType)  # O(1) space
```

## Creating Functions Dynamically

### FunctionType

#### Time Complexity: O(1)

```python
import types

# Create function: O(1)
def original_func(x):
    return x * 2

# Make copy of function: O(1)
new_func = types.FunctionType(
    original_func.__code__,
    original_func.__globals__,
)

result = new_func(5)  # 10 - O(1)

# Create with modified globals: O(1)
def factory(multiplier):
    def multiply(x):
        return x * multiplier
    return multiply

func2x = factory(2)
func3x = factory(3)
```

#### Space Complexity: O(1)

```python
import types

# New function object
new_func = types.FunctionType(code, globals)  # O(1) space
```

## Dynamic Namespaces

### SimpleNamespace

#### Time Complexity: O(n)

Where n = number of attributes.

```python
import types

# Create namespace: O(n) where n = attributes
ns = types.SimpleNamespace(
    name='Alice',
    age=30,
    city='NYC'
)

# Access attributes: O(1)
print(ns.name)  # 'Alice' - O(1)
ns.job = 'Engineer'  # O(1)

# Convert to dict: O(n)
data = vars(ns)  # {'name': 'Alice', 'age': 30, 'city': 'NYC'} - O(n)
```

#### Space Complexity: O(n)

```python
import types

ns = types.SimpleNamespace(a=1, b=2, c=3)  # O(n) space for attributes
```

## Read-Only Dictionaries

### MappingProxyType

#### Time Complexity: O(1)

```python
import types

# Create read-only view: O(1) - no copy, just wraps original
original = {'a': 1, 'b': 2, 'c': 3}
readonly = types.MappingProxyType(original)  # O(1)

# Access: O(1)
value = readonly['a']  # 1 - O(1)

# Length: O(1)
length = len(readonly)  # 3 - O(1)

# Iteration: O(n)
for key in readonly:  # O(n)
    print(key)

# Modification attempt: raises TypeError
# readonly['d'] = 4  # Error!
```

#### Space Complexity: O(1)

```python
import types

# Proxy (no copy): O(1) space
readonly = types.MappingProxyType(original)  # O(1) overhead
```

## Type Aliases

### Common Type Aliases

#### Time Complexity: O(1)

```python
import types

# Type checking with aliases: O(1)
if isinstance(obj, types.FunctionType):
    pass

if isinstance(obj, types.GeneratorType):
    pass

if isinstance(obj, types.CoroutineType):
    pass

if isinstance(obj, types.AsyncGeneratorType):
    pass

if isinstance(obj, types.LambdaType):  # Alias for FunctionType
    pass

if isinstance(obj, types.CodeType):
    pass

if isinstance(obj, types.TracebackType):
    pass

if isinstance(obj, types.FrameType):
    pass
```

#### Space Complexity: O(1)

```python
import types

is_func = isinstance(obj, types.FunctionType)  # O(1)
```

## Common Patterns

### Type Dispatch

```python
import types

def process(obj):
    """Process different types."""
    if isinstance(obj, types.FunctionType):
        return obj()
    elif isinstance(obj, types.GeneratorType):
        return list(obj)
    elif isinstance(obj, dict):
        return obj.items()
    else:
        return obj
```

### Create Config Object

```python
import types

def load_config(settings):
    """Convert dict to object."""
    return types.SimpleNamespace(**settings)  # O(n)

config = load_config({
    'host': 'localhost',
    'port': 8080,
    'debug': True,
})

print(config.host)  # O(1)
```

### Protected Configuration

```python
import types

# Create read-only config
config_dict = {
    'api_key': 'secret123',
    'database_url': 'postgresql://...',
    'debug': False,
}

config = types.MappingProxyType(config_dict)

# Can read: O(1)
key = config['api_key']

# Cannot modify: raises TypeError
# config['debug'] = True  # Error!

# Original can still be modified
config_dict['debug'] = True  # Still works
```

### Introspect Functions

```python
import types
import inspect

def analyze_function(func):
    """Analyze a function."""
    if isinstance(func, types.FunctionType):
        code = func.__code__
        print(f"Arguments: {code.co_argcount}")
        print(f"Variables: {code.co_varnames}")
        print(f"Constants: {code.co_consts}")
    return func

# Works with actual functions
@analyze_function
def greet(name):
    greeting = f"Hello, {name}"
    return greeting
```

## Performance Characteristics

### Best Practices

```python
import types

# Good: Use type aliases for clarity
if isinstance(obj, types.FunctionType):  # Clear intent
    call_function(obj)

# Good: Use SimpleNamespace for data objects
config = types.SimpleNamespace(x=1, y=2)  # Clean API

# Good: Use MappingProxyType for protection
immutable = types.MappingProxyType(data)  # Prevent accidents

# Avoid: Creating many function objects
for i in range(1000):
    new_func = types.FunctionType(code, globals)  # O(1000) total
```

### Memory Efficiency

```python
import types

# Good: MappingProxyType doesn't copy
original = {'a': 1, 'b': 2}
proxy = types.MappingProxyType(original)  # O(1) memory

# Avoid: Copying dict
copy = dict(original)  # O(n) memory copy
```

## Comparison with isinstance()

```python
import types

obj = (lambda x: x)  # Lambda function

# Using types module
isinstance(obj, types.FunctionType)  # O(1) - type constant

# Using type()
type(obj) == types.FunctionType  # O(1) - less Pythonic

# Using callable()
callable(obj)  # O(1) - but less specific
```

## Version Notes

- **Python 3.x**: Full type support
- **Python 3.7+**: `GenericAlias` for type hints
- **Python 3.10+**: Union type support

## Related Documentation

- [Inspect Module](inspect.md) - Object introspection
- [Operator Module](operator.md) - Operator functions
- [Collections.abc Module](collections.md) - Abstract base classes
