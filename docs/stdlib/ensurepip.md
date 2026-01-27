# ensurepip Module

The `ensurepip` module bootstraps the pip package installer into Python installations, ensuring pip is available.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `bootstrap()` | O(n) | O(n) | Install pip |
| `version()` | O(1) | O(1) | Return bundled pip version string |
| Verify | O(1) | O(1) | Check availability |

## Bootstrapping pip

### Ensuring pip is Available

```python
import ensurepip

# Bootstrap pip - O(n)
ensurepip.bootstrap()

# Optional arguments (all keyword-only) - O(n)
ensurepip.bootstrap(
    upgrade=True,      # upgrade bundled pip
    default_pip=True,  # install pip even if a "pipX" already exists
    verbosity=1,       # pass through to pip
)

# Or from command line:
# python -m ensurepip
# python -m ensurepip --upgrade
```

## Related Documentation

- [venv Module](venv.md)
- [pip Documentation](https://pip.pypa.io/)
