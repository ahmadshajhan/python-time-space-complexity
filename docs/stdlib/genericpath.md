# Genericpath Module Complexity

The `genericpath` module provides generic pathname utilities shared by `posixpath` and `ntpath`. It's part of the internal implementation but can be imported directly.

## Common Operations

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `commonprefix(list)` | O(n*m) | O(n) | Find common string prefix |
| `exists(path)` | O(1) | O(1) | Check if path exists |
| `lexists(path)` | O(1) | O(1) | Check if path exists (even if broken symlink) |
| `isfile(path)` | O(1) | O(1) | Check if file |
| `isdir(path)` | O(1) | O(1) | Check if directory |
| `islink(path)` | O(1) | O(1) | Check if symlink |
| `isjunction(path)` | O(1) | O(1) | Check Windows junction |
| `isdevdrive(path)` | O(1) | O(1) | Check Windows Dev Drive |
| `getsize(path)` | O(1) | O(1) | Get file size |
| `getmtime(path)` | O(1) | O(1) | Get modification time |
| `getatime(path)` | O(1) | O(1) | Get access time |
| `getctime(path)` | O(1) | O(1) | Get creation time |
| `samefile(a, b)` | O(1) | O(1) | Compare underlying file identity |
| `samestat(stat1, stat2)` | O(1) | O(1) | Compare stat results |
| `sameopenfile(fd1, fd2)` | O(1) | O(1) | Compare open file descriptors |

## Path Comparison

### commonprefix()

#### Time Complexity: O(n*m)

```python
import genericpath

# Find common prefix: O(n*m) character comparison
paths = ['prefix/path1', 'prefix/path2', 'prefix/other']
prefix = genericpath.commonprefix(paths)  # O(n*m)
# Result: 'prefix/'

# All same
prefix = genericpath.commonprefix(['abc', 'abc', 'abc'])  # O(n*m)
# Result: 'abc'

# No common prefix
prefix = genericpath.commonprefix(['xyz', 'abc'])  # O(n*m)
# Result: ''
```

#### Space Complexity: O(m)

```python
import genericpath

paths = ['a' * 1000, 'a' * 1000, 'b' * 1000]
prefix = genericpath.commonprefix(paths)  # O(m) space for result
```

File identity helpers can compare paths or stat results:

```python
import genericpath
import os

same = genericpath.samefile("a.txt", "b.txt")  # O(1)
same = genericpath.sameopenfile(os.open("a.txt", os.O_RDONLY),
                                os.open("a.txt", os.O_RDONLY))  # O(1)
stat1 = os.stat("a.txt")
stat2 = os.stat("b.txt")
same = genericpath.samestat(stat1, stat2)  # O(1)
```

## Path Existence and Type Checks

### exists(), lexists(), isfile(), isdir()

#### Time Complexity: O(1)

```python
import genericpath

# Single stat call: O(1)
if genericpath.exists('/path/to/file'):  # O(1) stat
    print('exists')

if genericpath.lexists('/path/to/maybe-link'):  # O(1) lstat
    print('exists (even if broken symlink)')

if genericpath.isfile('/path/to/file'):  # O(1) stat
    print('is file')

if genericpath.isdir('/path/to/dir'):  # O(1) stat
    print('is directory')

# Multiple checks: O(k) where k = checks
for path in paths:  # k paths
    if genericpath.exists(path):  # O(1) per check
        process(path)
```

#### Space Complexity: O(1)

```python
import genericpath

# No additional storage
result = genericpath.exists('/path')  # O(1) space
```

### islink()

#### Time Complexity: O(1)

```python
import genericpath

# Check if symlink: O(1) lstat
if genericpath.islink('/path/to/link'):  # O(1)
    print('is symlink')
```

#### Space Complexity: O(1)

```python
import genericpath

is_link = genericpath.islink('/path')  # O(1) space
```

Windows-only checks also include junctions and Dev Drives:

```python
import genericpath

if genericpath.isjunction('C:\\\\path\\\\to\\\\junction'):  # O(1)
    print('is junction')

if genericpath.isdevdrive('C:\\\\path'):  # O(1)
    print('is dev drive')
```

## File Statistics

### getsize(), getmtime(), getatime(), getctime()

#### Time Complexity: O(1)

```python
import genericpath

# Get file size: O(1) stat call
size = genericpath.getsize('/path/file.txt')  # O(1)

# Get modification time: O(1)
mtime = genericpath.getmtime('/path/file.txt')  # O(1)

# Get access time: O(1)
atime = genericpath.getatime('/path/file.txt')  # O(1)

# Get creation time: O(1)
ctime = genericpath.getctime('/path/file.txt')  # O(1)

# Multiple stats: O(k) where k = files
for file in files:  # k files
    size = genericpath.getsize(file)  # O(1) per file
```

#### Space Complexity: O(1)

```python
import genericpath

# Single numeric value returned
size = genericpath.getsize('/path')  # O(1) space
```

## Common Patterns

### Find Common Path Base

```python
import genericpath

# Compare file paths: O(n*m)
paths = [
    '/home/user/docs/file1.txt',
    '/home/user/docs/file2.txt',
    '/home/user/downloads/file3.txt',
]

common = genericpath.commonpath(paths)  # O(n*m)
# Result: '/home/user'

# Use for batch operations on directory
print(f'All files under: {common}')
```

### Verify Files Before Processing

```python
import genericpath

def process_files_safely(file_list):
    # Check all exist: O(n)
    for file in file_list:
        if not genericpath.exists(file):  # O(1) each
            raise FileNotFoundError(file)
    
    # Process files
    for file in file_list:
        if genericpath.isfile(file):  # O(1)
            process(file)
```

### Check File Sizes

```python
import genericpath

def get_total_size(file_list):
    """Get total size of files: O(n)"""
    total = 0
    for file in file_list:
        if genericpath.isfile(file):  # O(1)
            total += genericpath.getsize(file)  # O(1)
    return total

size = get_total_size(files)  # O(n) where n = files
```

### Find Recently Modified Files

```python
import genericpath
import time

def find_recent_files(file_list, hours=24):
    """Find recently modified files: O(n)"""
    cutoff = time.time() - (hours * 3600)
    recent = []
    
    for file in file_list:
        if not genericpath.isfile(file):  # O(1)
            continue
        
        mtime = genericpath.getmtime(file)  # O(1)
        if mtime > cutoff:
            recent.append(file)
    
    return recent  # O(n) total
```

## Performance Characteristics

### Best Practices

```python
import genericpath

# Good: Cache results
exists = genericpath.exists(path)  # O(1)
if exists:
    size = genericpath.getsize(path)  # O(1)
    # Use cached knowledge

# Avoid: Repeated checks
if genericpath.exists(path):  # O(1)
    if genericpath.isfile(path):  # O(1) - second stat!
        process(path)

# Better: Use isfile() only (does stat once)
if genericpath.isfile(path):  # O(1)
    process(path)
```

### Batch Operations

```python
import genericpath

# Good: Single pass for multiple checks
for file in files:  # O(n) total
    if genericpath.exists(file):  # O(1) each
        size = genericpath.getsize(file)  # O(1) each
        # Total: O(n)

# Avoid: Multiple iterations
for file in files:
    if genericpath.exists(file):  # O(n) - first pass
        pass

for file in files:
    size = genericpath.getsize(file)  # O(n) - second pass
```

## Comparison with pathlib

```python
import genericpath
from pathlib import Path

# genericpath (functional)
exists = genericpath.exists(path)  # O(1)
size = genericpath.getsize(path)   # O(1)
mtime = genericpath.getmtime(path) # O(1)

# pathlib (object-oriented)
path_obj = Path(path)
exists = path_obj.exists()          # O(1)
size = path_obj.stat().st_size      # O(1)
mtime = path_obj.stat().st_mtime    # O(1)

# Similar complexity, pathlib caches stat()
```

## Comparison with os module

```python
import genericpath
import os

# genericpath
exists = genericpath.exists(path)  # O(1)
size = genericpath.getsize(path)   # O(1)

# os module (similar but os.stat is more direct)
stat_info = os.stat(path)  # O(1)
exists = stat_info is not None
size = stat_info.st_size

# Both O(1), os.stat more flexible
```

`ALLOW_MISSING` is a public sentinel used by `os.path.realpath()` to allow missing path components.

## Platform Independence

```python
import genericpath

# Works cross-platform (uses stat underneath)
path = '/home/user/file.txt'  # or 'C:\\Users\\user\\file.txt'

exists = genericpath.exists(path)  # O(1) on any platform
size = genericpath.getsize(path)   # O(1) on any platform
```


## Version Notes

- **Python 3.x**: Full Unicode support
- **All versions**: Low-level interface to os.stat()

## Related Documentation

- [Pathlib Module](pathlib.md) - Object-oriented paths
- [Posixpath Module](posixpath.md) - Unix-specific paths
- [Ntpath Module](ntpath.md) - Windows-specific paths
- [OS Module](os.md) - Operating system interface
