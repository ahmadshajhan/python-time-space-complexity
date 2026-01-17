# distutils Module

The `distutils` module provides tools for building and distributing Python packages (deprecated in favor of setuptools and modern packaging tools).

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Build distribution | O(n) | O(n) | n = files |
| Compile extensions | O(k) | O(k) | k = C files |

## Building Distributions

### Setup Script

```python
from distutils.core import setup

setup(
    name='mypackage',
    version='1.0.0',
    description='My package',
    author='Your Name',
    py_modules=['mymodule'],
    scripts=['bin/myscript'],
)

# Run:
# python setup.py build
# python setup.py install
# python setup.py sdist
```

## Related Documentation

- [setuptools Library](https://pypi.org/project/setuptools/)
- [venv Module](venv.md)
