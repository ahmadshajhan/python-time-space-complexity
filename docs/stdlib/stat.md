# stat Module

The `stat` module provides constants and functions for interpreting file stat results from os.stat() and related functions.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Mode check | O(1) | O(1) | Bitwise operation |
| `filemode()` | O(1) | O(1) | Convert mode to string |

## File Mode Operations

### Checking File Types

```python
import os
import stat

# Get file stats - O(1)
file_stat = os.stat('myfile.txt')

# Check file type - O(1)
if stat.S_ISREG(file_stat.st_mode):
    print("Regular file")
elif stat.S_ISDIR(file_stat.st_mode):
    print("Directory")
elif stat.S_ISLNK(file_stat.st_mode):
    print("Symbolic link")

# Convert to string - O(1)
mode_str = stat.filemode(file_stat.st_mode)
print(mode_str)  # e.g., "-rw-r--r--"
```

### Checking Permissions

```python
import os
import stat

file_stat = os.stat('script.py')

# Check permissions - O(1)
if file_stat.st_mode & stat.S_IEXEC:
    print("Executable")

if file_stat.st_mode & stat.S_IWRITE:
    print("Writable")
```

## Related Documentation

- [os Module](os.md)
- [pathlib Module](pathlib.md)
