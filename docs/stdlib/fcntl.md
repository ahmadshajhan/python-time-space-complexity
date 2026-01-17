# fcntl Module

The `fcntl` module provides access to file control operations on Unix, including file locking and other low-level file I/O control.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `flock()` | O(1) | O(1) | Acquire lock |
| `fcntl()` | O(1) | O(1) | File control |

## File Locking and Control

### File Locking

```python
import fcntl

# Open file
with open('data.txt', 'w') as f:
    # Acquire lock - O(1)
    fcntl.flock(f.fileno(), fcntl.LOCK_EX)
    
    try:
        # Write while locked
        f.write('Protected data')
    finally:
        # Release lock - O(1)
        fcntl.flock(f.fileno(), fcntl.LOCK_UN)
```

### Non-blocking Lock

```python
import fcntl

with open('file.txt', 'r') as f:
    try:
        # Non-blocking exclusive lock - O(1)
        fcntl.flock(f.fileno(), fcntl.LOCK_EX | fcntl.LOCK_NB)
        print("Lock acquired")
    except BlockingIOError:
        print("File is locked by another process")
```

## Related Documentation

- [os Module](os.md)
- [threading Module](threading.md)
