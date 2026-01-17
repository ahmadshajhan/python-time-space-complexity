# nturl2path Module

The `nturl2path` module converts between Windows file paths and URL paths, handling Windows-specific path conventions.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `url2pathname()` | O(n) | O(n) | n = path length |
| `pathname2url()` | O(n) | O(n) | n = path length |

## Converting Paths

### URL to Windows Path

```python
import nturl2path

# Convert URL to path - O(n)
path = nturl2path.url2pathname('/C|/Users/Alice/file.txt')
print(path)  # C:\\Users\\Alice\\file.txt

# Convert path to URL - O(n)
url = nturl2path.pathname2url('C:\\\\Users\\\\Alice\\\\file.txt')
print(url)  # /C|/Users/Alice/file.txt
```

## Related Documentation

- [pathlib Module](pathlib.md)
- [urllib.request Module](urllib.md)
