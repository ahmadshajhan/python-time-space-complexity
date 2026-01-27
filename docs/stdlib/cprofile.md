# cProfile Module

The `cProfile` module provides deterministic profiling of Python programs, measuring function call frequency and execution time.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `cProfile.run()` | O(n) | O(n) | n = function calls |
| `cProfile.runctx()` | O(n) | O(n) | n = function calls; with globals/locals |
| `cProfile.main()` | O(n) | O(n) | CLI entrypoint |
| `Profile()` | O(1) | O(1) | Profiler instance |
| Profile collection | O(1) | O(1) | Per call overhead |
| Report generation | O(n log n) | O(n) | n = unique functions |

## Profiling Functions

### Basic Profiling

```python
import cProfile

def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# Profile function - O(n) where n = calls
cProfile.run('fibonacci(10)')

# Output shows: ncalls, tottime, cumtime, filename:lineno(function)
```

### Analyzing Profile Data

```python
import cProfile
import pstats

# Profile with save - O(n)
cProfile.run('fibonacci(10)', 'profile_stats')

# Load and analyze - O(n log n)
stats = pstats.Stats('profile_stats')
stats.strip_dirs()
stats.sort_stats('cumulative')
stats.print_stats(10)  # Top 10
```

## Related Documentation

- [profile Module](profile.md)
- [pstats Module](pstats.md)
- [timeit Module](timeit.md)
