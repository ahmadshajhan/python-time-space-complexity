# zipapp Module

The `zipapp` module creates executable ZIP applications that can be run directly as Python scripts, bundling code and dependencies.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Create archive | O(n) | O(n) | n = total files |
| Pack app | O(n) | O(n) | ZIP compression |

## Creating ZIP Applications

### Building Executable Archive

```python
import zipapp

# Create zipapp - O(n)
zipapp.create_archive(
    'myapp',
    target='myapp.pyz',
    main='myapp:main',
    compression='deflated'
)

# Run:
# python myapp.pyz
# or
# ./myapp.pyz  (with shebang)
```

### Command-line Usage

```bash
# Create app from directory
python -m zipapp myapp -m myapp:main -o app.pyz

# Make executable
chmod +x app.pyz

# Run
./app.pyz
```

## Related Documentation

- [zipfile Module](zipfile.md)
- [venv Module](venv.md)
