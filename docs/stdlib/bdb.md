# bdb Module

The `bdb` module provides a generic debugger framework that higher-level debuggers like pdb build upon.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `Bdb()` setup | O(1) | O(1) | Initialize debugger |
| Set breakpoint | O(1) | O(1) | Register break |
| Continue | O(n) | O(n) | n = traced instructions |
| `Breakpoint` creation | O(1) | O(1) | Track location/condition |
| `BdbQuit` | O(1) | O(1) | Exception used to quit debugger |
| `set_trace()` | O(1) | O(1) | Install tracer at current frame |
| `effective()` | O(k) | O(1) | k = breakpoints at location |
| `checkfuncname()` | O(1) | O(1) | Match function name to frame |
| `Tdb()` setup | O(1) | O(1) | Traceback debugger |
| `foo()` / `bar()` | O(1) | O(1) | Demo functions (constant work) |
| `test()` | O(1) | O(1) | Demo entrypoint; runs debugger |
| `E` | O(1) | O(1) | Event flag namespace |

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

## Breakpoint Resolution Cost

`effective()` scans the breakpoint list for a location and returns the
first enabled match. The runtime cost is linear in the number of
breakpoints registered for that line (O(k)).


## Related Documentation

- [pdb Module](pdb.md)
- [sys Module](sys.md)
