# compileall Module

The `compileall` module compiles all Python source files in a directory tree to bytecode (.pyc files).

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `compile_dir()` | O(n) | O(n) | n = .py files |
| Compile file | O(m) | O(m) | m = file size |
| `compile_file()` | O(m) | O(m) | Compile one file |
| `compile_path()` | O(n) | O(n) | n = files on sys.path |
| `main()` | O(n) | O(n) | CLI entrypoint |

## Batch Compiling Python Files

### Compile Directory

```python
import compileall

# Compile directory tree - O(n)
compileall.compile_dir('/path/to/code')

# With options
compileall.compile_dir(
    '/path/to/code',
    force=True,        # Recompile all
    quiet=0            # Show progress
)

# Or from command line:
# python -m compileall /path/to/code
```

### Compile Single File

```python
import py_compile

# Compile one file - O(m)
py_compile.compile('myfile.py')
```

## Related Documentation

- [py_compile Module](py_compile.md)
- [ast Module](ast.md)
