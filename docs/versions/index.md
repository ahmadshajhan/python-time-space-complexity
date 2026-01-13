# Python Version Guides

Different Python versions have made various optimizations and changes that affect complexity characteristics.

## Version Overview

| Version | Release | Status | Notes |
|---------|---------|--------|-------|
| 3.8 | Oct 2019 | Security fixes | Assignment expressions (walrus) |
| 3.9 | Oct 2020 | Security fixes | Type hints, new parsers |
| 3.10 | Oct 2021 | Bugfix | Pattern matching |
| 3.11 | Oct 2022 | Current | Inline caching, 10-60% faster |
| 3.12 | Oct 2023 | Current | Better specialization |

## Quick Links

- **[Python 3.12](py312.md)** - Latest version with new optimizations
- **[Python 3.11](py311.md)** - Significant performance improvements (inline caching)
- **[Python 3.10](py310.md)** - Pattern matching additions
- **[Python 3.9](py39.md)** - Type hints and parser improvements

## Key Changes by Version

### Python 3.12 (October 2023)

New features and optimizations:

```python
# Improved error messages
"test"[999]  # IndexError with better message

# Type parameter syntax (PEP 695)
def greet[T: str](x: T) -> T:
    return x

# Performance: 5-10% faster on average
```

### Python 3.11 (October 2022)

Major performance improvements:

```python
# Exception groups and except* syntax
try:
    ...
except ExceptionGroup as eg:
    raise eg.derive(...)

# Inline caching for attributes
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

p = Point(1, 2)
# First access: cache miss
print(p.x)
# Repeated access: uses inline cache (much faster)

# 10-60% performance improvement overall
```

### Python 3.10 (October 2021)

Pattern matching:

```python
# Structural pattern matching
match value:
    case 1:
        print("one")
    case 2:
        print("two")
    case _:
        print("other")
```

### Python 3.9 (October 2020)

Type hints and flexibility:

```python
# Type hints without import
def add(a: list[int], b: list[int]) -> list[int]:
    return [x + y for x, y in zip(a, b)]

# Dictionary operations
d1 = {'a': 1}
d2 = {'b': 2}
d3 = d1 | d2  # {' a': 1, 'b': 2}
d1 |= d2  # Update in place
```

### Python 3.8 (October 2019)

Assignment expressions:

```python
# Walrus operator :=
if (n := len(a)) > 10:
    print(f"List too long ({n} elements)")

# Positional-only parameters
def func(x, /, y):
    # x is positional-only, y can be keyword
    pass
```

## Compatibility Considerations

### End of Life Dates

| Version | EOL Date |
|---------|----------|
| 3.8 | Oct 2024 |
| 3.9 | Oct 2025 |
| 3.10 | Oct 2026 |
| 3.11 | Oct 2027 |
| 3.12 | Oct 2028 |

Plan upgrades before EOL.

### Breaking Changes

Generally minimal between minor versions, but check:

- [Python 3.10 What's New](https://docs.python.org/3.10/whatsnew/)
- [Python 3.11 What's New](https://docs.python.org/3.11/whatsnew/)
- [Python 3.12 What's New](https://docs.python.org/3.12/whatsnew/)

## Performance Recommendations

### Upgrade Path

```
Python 3.8 → Python 3.9    Incremental improvements
Python 3.9 → Python 3.10   Minor improvements
Python 3.10 → Python 3.11  10-60% faster (significant!)
Python 3.11 → Python 3.12  5-10% faster
```

**Recommendation**: Use Python 3.11+ for performance.

## Feature by Version

| Feature | Version | Status |
|---------|---------|--------|
| Walrus operator | 3.8+ | Stable |
| Type hints (generic) | 3.9+ | Stable |
| Pattern matching | 3.10+ | Stable |
| Inline caching | 3.11+ | Stable |
| Exception groups | 3.11+ | Stable |
| Type parameters | 3.12+ | New |

## Complexity Characteristics by Version

### Dict Operations

| Version | Behavior | Complexity |
|---------|----------|-----------|
| 3.5 | Unordered | O(1) lookup |
| 3.6+ | Ordered | O(1) lookup |
| 3.9+ | Optimized | O(1) lookup (faster) |

### List Operations

| Version | Append | Insert | Notes |
|---------|--------|--------|-------|
| All 3.x | O(1)* | O(n) | Consistent |

### String Operations

| Version | Lookup | Contains | Notes |
|---------|--------|----------|-------|
| 3.3+ | O(1) | O(n*m) | Flexible representation |
| 3.11+ | O(1) | O(n*m)* | Faster due to inline caching |

## Upgrading Python

### Check Compatibility

```bash
# Test with newer version
pyenv install 3.12.0
pyenv shell 3.12.0
python -m pytest  # Run tests

# Check for deprecations
python -W all your_script.py
```

### Gradual Adoption

```bash
# Keep older version
pyenv install 3.11.0
pyenv local 3.11.0  # Use 3.11 for this project
pyenv global 3.12.0  # Use 3.12 everywhere else
```

## Related Documentation

- [CPython Implementation](../implementations/cpython.md)
- [Built-in Types](../builtins/index.md)
- [Standard Library](../stdlib/index.md)
