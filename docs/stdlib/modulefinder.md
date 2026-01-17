# modulefinder Module

The `modulefinder` module finds all modules that a Python script imports, useful for analyzing dependencies and creating standalone applications.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Find dependencies | O(n) | O(n) | n = imported modules |
| Build import graph | O(n) | O(n) | Track relationships |

## Analyzing Module Dependencies

### Finding Imported Modules

```python
from modulefinder import ModuleFinder

# Create finder - O(1)
mf = ModuleFinder()

# Analyze script - O(n)
mf.run_script('myapp.py')

# Get results - O(1)
print("Modules:", mf.modules)
print("Bad imports:", mf.badimports)

# Report - O(n)
mf.report()
```

## Related Documentation

- [importlib Module](importlib.md)
- [ast Module](ast.md)
