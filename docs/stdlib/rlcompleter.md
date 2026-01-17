# rlcompleter Module

The `rlcompleter` module provides command-line completion for the Python interactive interpreter using readline.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `RLCompleter()` | O(n) | O(n) | n = namespace |
| Completion | O(n) | O(n) | Match suggestions |

## Readline Completion

### Interactive Completion Setup

```python
import readline
import rlcompleter

# Create completer - O(n)
completer = rlcompleter.RLCompleter()

# Install completer - O(1)
readline.set_completer(completer.complete)

# Enable tab completion - O(1)
readline.parse_and_bind('tab: complete')

# In Python interactive mode:
# >>> import math
# >>> math.<TAB>  # Shows completions
```

## Related Documentation

- [readline Module](readline.md)
- [code Module](code.md)
