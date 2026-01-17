# keyword Module

The `keyword` module provides access to Python's set of keywords and allows checking if a string is a keyword.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `keyword.iskeyword()` | O(1) | O(1) | Hash-based lookup |
| Access keyword list | O(1) | O(1) | Pre-computed |

## Checking for Keywords

### Is String a Keyword

```python
import keyword

# Check if keyword - O(1)
print(keyword.iskeyword('if'))      # True
print(keyword.iskeyword('else'))    # True
print(keyword.iskeyword('variable')) # False

# List all keywords - O(1) access
print(keyword.kwlist)
# ['False', 'None', 'True', 'and', 'as', 'assert', ...]
```

## Related Documentation

- [token Module](token.md)
- [tokenize Module](tokenize.md)
