# trace Module

The `trace` module provides tracing of program execution and coverage analysis, showing which lines of code are executed.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `Trace.run()` | O(n) | O(n) | n = bytecode instructions; significant overhead per line |
| Coverage analysis | O(n) | O(n) | Track executed lines; stores line counts |

## Program Tracing

### Basic Execution Tracing

```python
import trace

def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# Create tracer - O(1)
tracer = trace.Trace(count=False, trace=True)

# Run with trace - O(n)
tracer.run('fibonacci(5)')

# Output shows each line executed
```

### Coverage Analysis

```python
import trace

def calculate(x, y):
    result = x + y
    unused = x * y  # This line might not execute
    return result

# Create coverage tracer - O(1)
tracer = trace.Trace(count=True, trace=False)

# Run - O(n)
tracer.run('calculate(2, 3)')

# Get results - O(1)
results = tracer.results()
results.write_results(show_missing=True)
```

## Related Documentation

- [sys Module](sys.md)
- [dis Module](dis.md)
