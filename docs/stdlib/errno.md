# errno Module

The `errno` module provides platform-specific error number constants and an `errorcode` mapping
for converting between numeric error codes and their symbolic names.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Access `E*` constant | O(1) | O(1) | Integer constant lookup |
| `errorcode[err]` | O(1) | O(1) | Dict lookup for symbolic name |
| Compare `exc.errno` | O(1) | O(1) | Integer compare |

!!! warning "Platform-dependent constants"
    `errno` values are OS-dependent. Some constants may be missing or have different numeric
    values across platforms.

## Common Operations

### Check an `OSError` by errno

```python
import errno

try:
    with open("missing.txt", "r") as handle:
        data = handle.read()
except OSError as exc:
    if exc.errno == errno.ENOENT:
        print("File not found")
    elif exc.errno == errno.EACCES:
        print("Permission denied")
    else:
        raise
```

### Map an error code to its name

```python
import errno

# O(1) lookup
name = errno.errorcode[errno.ENOENT]  # "ENOENT"
```

### Use errno in filesystem helpers

```python
import errno
import os

try:
    os.remove("tmp.txt")
except FileNotFoundError as exc:
    # FileNotFoundError derives from OSError
    if exc.errno == errno.ENOENT:
        pass
```

## Public Constants

The module exposes many `E*` integer constants such as:

- `EACCES`, `EEXIST`, `EINVAL`, `EIO`, `ENOENT`, `ENOSPC`, `ENOTDIR`, `EPIPE`
- Socket-related errors like `ECONNRESET`, `ECONNREFUSED`, `ETIMEDOUT`

Use `dir(errno)` to list all constants available on your platform.

## Related Documentation

- [os Module](os.md)
- [stat Module](stat.md)
- [pathlib Module](pathlib.md)
