# pydoc_data Module

The `pydoc_data` module contains static documentation data files used by pydoc for generating help text and documentation.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Load data | O(1) | O(n) | n = docs size |

## Documentation Data

### Pydoc Data Files

```python
# pydoc_data is used internally by pydoc
# Not meant for direct use, but contains:
# - Module documentation
# - Help topics
# - Topic index

# Access via pydoc:
import pydoc
pydoc.help('topics')  # List help topics
pydoc.help('MODULES') # Module index
```

## Related Documentation

- [pydoc Module](pydoc.md)
- [help() Function](../builtins/index.md)
