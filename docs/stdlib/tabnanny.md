# tabnanny Module

The `tabnanny` module checks Python source files for mixed tabs and spaces in indentation, which can cause syntax errors.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Check file/directory | O(n) | O(d) | n = file tokens scanned, d = max indent depth |

## Checking Indentation

### Checking File for Tab Issues

```python
import tabnanny

# Check file - O(n)
tabnanny.check('myfile.py')  # Prints diagnostics to stdout; returns None

# Or from command line:
# python -m tabnanny myfile.py
```

## Related Documentation

- [tokenize Module](tokenize.md)
- [inspect Module](inspect.md)
