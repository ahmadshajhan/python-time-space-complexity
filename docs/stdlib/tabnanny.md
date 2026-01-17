# tabnanny Module

The `tabnanny` module checks Python source files for mixed tabs and spaces in indentation, which can cause syntax errors.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Check file | O(n) | O(n) | n = file lines |
| Verify indent | O(1) | O(1) | Per line |

## Checking Indentation

### Checking File for Tab Issues

```python
import tabnanny

# Check file - O(n)
result = tabnanny.check('myfile.py')

# Returns True if issues found
if result:
    print("File has tab/space issues")

# Or from command line:
# python -m tabnanny myfile.py
```

## Related Documentation

- [tokenize Module](tokenize.md)
- [inspect Module](inspect.md)
