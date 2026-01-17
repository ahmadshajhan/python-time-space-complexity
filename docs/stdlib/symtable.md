# symtable Module

The `symtable` module provides access to Python's internal symbol table, showing information about variables, scopes, and declarations.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `symtable()` | O(n) | O(n) | n = code size |
| Build symbol table | O(n) | O(n) | Analyze scopes |

## Analyzing Symbol Tables

### Getting Symbol Information

```python
import symtable

code = """
x = 10
def func(a, b):
    y = a + b
    return y
"""

# Create symbol table - O(n)
table = symtable.symtable(code, '<string>', 'exec')

# Get info - O(1)
print(table.get_name())        # Module name
print(table.get_symbols())      # All symbols

# Get symbol - O(1)
sym = table.lookup('x')
print(sym.is_global())
print(sym.is_local())

# Get nested scopes - O(1)
children = table.get_children()  # Functions, classes
```

## Related Documentation

- [ast Module](ast.md)
- [inspect Module](inspect.md)
