# zipimport Module

The `zipimport` module enables importing Python modules and packages directly from ZIP files without extraction.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `zipimporter()` | O(n) | O(n) | n = ZIP size |
| Import module | O(log n) | O(1) | Binary search in ZIP |
| Load bytecode | O(1) | O(n) | n = module size |

## Importing from ZIP Files

### Using ZIP Importer

```python
import sys
import zipimport

# Add ZIP to path - O(1)
sys.path.insert(0, '/path/to/archive.zip')

# Import from ZIP - O(log n)
import mymodule

# Call module functions
result = mymodule.function()
```

### Creating ZIP Importer

```python
import zipimport

# Create importer - O(n)
importer = zipimport.zipimporter('/path/to/archive.zip')

# Get module code - O(log n)
code = importer.get_code('mymodule')

# Load module - O(1)
spec = importer.find_spec('mymodule')
```

## Related Documentation

- [importlib Module](importlib.md)
- [zipfile Module](zipfile.md)
