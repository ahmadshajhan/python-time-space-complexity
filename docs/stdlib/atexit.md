# atexit Module Complexity

The `atexit` module registers functions to run when the interpreter terminates
normally. Handlers run in last-in, first-out (LIFO) order.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `atexit.register()` | O(1) | O(1) | Append handler to stack |
| `atexit.unregister()` | O(n) | O(1) | n = registered handlers; removes all matches |
| Handler execution | O(n) | O(1) | n = registered handlers; LIFO order |

!!! warning "When handlers run"
    Handlers run only on normal interpreter shutdown (e.g., program end or
    `sys.exit()`). They do not run on `os._exit()` or hard termination signals.

## Registering Cleanup Handlers

```python
import atexit

# Register handler - O(1)
@atexit.register
def cleanup():
    print("Cleaning up")
```

## Handler Order (LIFO)

```python
import atexit

@atexit.register
def first():
    print("first")

@atexit.register
def second():
    print("second")

# On shutdown:
# second
# first
```

## Unregistering Handlers

```python
import atexit

def temp():
    pass

atexit.register(temp)
atexit.unregister(temp)  # O(n) scan to remove all matches
```

## Related Documentation

- [sys Module](sys.md)
- [signal Module](signal.md)
