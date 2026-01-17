# pdb Module

The `pdb` module provides an interactive debugger for Python code, allowing breakpoints, stepping, and inspection of variables.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `set_trace()` | O(1) | O(1) | Enter debugger |
| Breakpoint | O(1) | O(1) | Register break |
| Step/continue | O(1) | O(1) | Control flow |

## Interactive Debugging

### Setting Breakpoints

```python
import pdb

def buggy_function(x):
    # Enter debugger - O(1)
    pdb.set_trace()
    
    result = x * 2
    return result

# When called, drops into interactive debugger
# Commands: n=next, s=step, c=continue, l=list, p=print
```

### Post-Mortem Debugging

```python
import pdb
import traceback

try:
    1 / 0
except Exception:
    # Debug after exception - O(1)
    pdb.post_mortem()
```

## Related Documentation

- [traceback Module](traceback.md)
- [inspect Module](inspect.md)
