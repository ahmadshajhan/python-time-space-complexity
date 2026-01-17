# bdb Module

The `bdb` module provides a generic debugger framework that higher-level debuggers like pdb build upon.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `Bdb()` setup | O(1) | O(1) | Initialize debugger |
| Set breakpoint | O(1) | O(1) | Register break |
| Continue | O(n) | O(n) | n = instructions |

## Debugger Framework

### Creating Custom Debugger

```python
import bdb

class MyDebugger(bdb.Bdb):
    def user_line(self, frame):
        # Called at each line - O(1)
        print(f"Line {frame.f_lineno}: {frame.f_code.co_name}")
    
    def user_return(self, frame, return_value):
        # Called on return - O(1)
        print(f"Returning: {return_value}")

# Use debugger - O(n)
debugger = MyDebugger()
debugger.run('function_to_debug()')
```

## Related Documentation

- [pdb Module](pdb.md)
- [sys Module](sys.md)
