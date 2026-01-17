# doctest Module

The `doctest` module finds and runs tests embedded in docstrings. It extracts example code from docstrings and verifies the output matches.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `doctest.testmod()` | O(n) | O(n) | n = docstring lines |
| Example extraction | O(n) | O(n) | Parse docstrings |
| Test execution | O(k) | O(1) | k = number of examples |

## Running Doctests

### Basic Doctest

```python
import doctest

def add(a, b):
    """
    Add two numbers.
    
    >>> add(2, 3)
    5
    >>> add(-1, 1)
    0
    """
    return a + b

# Run tests - O(n) where n = docstring examples
doctest.testmod(verbose=True)
# Trying: add(2, 3)
# Expecting: 5
# ok
```

### Testing with Output

```python
import doctest

def greet(name):
    """
    Greet someone.
    
    >>> greet('Alice')
    'Hello, Alice!'
    >>> greet('Bob')
    'Hello, Bob!'
    """
    return f"Hello, {name}!"

# Test - O(n)
results = doctest.testmod()
print(f"Tests: {results.attempted}, Failures: {results.failed}")
```

## Running Doctests on Modules

### Module-Level Testing

```python
import doctest
import mymodule

# Run all doctests in module - O(n)
doctest.testmod(mymodule, verbose=True)

# Or from command line:
# python -m doctest mymodule.py -v
```

## Related Documentation

- [unittest Module](unittest.md)
- [inspect Module](inspect.md)
