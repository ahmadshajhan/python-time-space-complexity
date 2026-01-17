# stringprep Module

The `stringprep` module provides support for internationalized domain names through Unicode normalization and validation per RFC 3454.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `prepare()` | O(n) | O(n) | n = string length |
| Character mapping | O(1) | O(1) | Hash lookup |

## String Preparation

### Preparing Unicode Strings

```python
import stringprep

# Prepare for use - O(n)
username = stringprep.nameprep('Müller')

# Prepare domain names
domain = stringprep.nameprep('münchen.de')

# Results are normalized
print(username)  # Normalized form
```

## Related Documentation

- [codecs Module](codecs.md)
- [unicodedata Module](../builtins/str.md)
