# pydoc Module

The `pydoc` module generates automatic documentation for Python modules from their docstrings, providing CLI and GUI interfaces.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Generate docs | O(n) | O(n) | n = module objects |
| Format text | O(n) | O(n) | n = docstring length |

## Generating Documentation

### Command-Line Help

```python
import pydoc

# Get help text - O(n)
help_text = pydoc.render_doc('os')
print(help_text)

# Or from command line:
# python -m pydoc os
```

### Serving Documentation

```bash
# Start documentation server - O(1) setup
python -m pydoc -p 8000
# Access at http://localhost:8000
```

## Related Documentation

- [inspect Module](inspect.md)
- [doctest Module](doctest.md)
