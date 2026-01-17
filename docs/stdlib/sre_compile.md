# sre_compile Module

The `sre_compile` module handles the internal compilation of regular expression patterns to bytecode (used internally by `re` module).

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Compile pattern | O(n) | O(n) | n = pattern length |
| Generate bytecode | O(n) | O(n) | n = pattern complexity |

## Regular Expression Compilation

### Examining Compiled Patterns

```python
import re
import sre_compile

# Compile pattern - O(n)
pattern = re.compile(r'\d+')

# Access bytecode - O(1)
bytecode = pattern.pattern
print(bytecode)

# Get pattern info
print(pattern.groups)      # Number of groups
print(pattern.groupindex)  # Named group indices
```

## Related Documentation

- [re Module](re.md)
- [sre_parse Module](sre_parse.md)
- [sre_constants Module](sre_constants.md)
