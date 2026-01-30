# time Module

The `time` module provides time-related functions for wall-clock time, monotonic clocks, sleep,
and conversions between timestamps and struct_time.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `time()` | O(1) | O(1) | Current wall-clock time (seconds since epoch) |
| `sleep(s)` | O(1) | O(1) | Blocks for at least s seconds |
| `monotonic()` | O(1) | O(1) | Monotonic clock, not subject to system clock changes |
| `perf_counter()` | O(1) | O(1) | High-resolution performance counter |
| `process_time()` | O(1) | O(1) | CPU time for the current process |
| `gmtime(t)` / `localtime(t)` | O(1) | O(1) | Convert timestamp to `struct_time` |
| `mktime(tuple)` | O(1) | O(1) | Convert local time tuple to timestamp |
| `asctime(t)` / `ctime(t)` | O(1) | O(1) | Format fixed-width time string |
| `strftime(fmt, t)` | O(n) | O(n) | n = output length |
| `strptime(s, fmt)` | O(n) | O(n) | n = input length |

## Getting Current Time

```python
import time

# Wall-clock time (seconds since epoch)
now = time.time()  # O(1)

# Monotonic clock for measuring durations
start = time.monotonic()  # O(1)
# ... do work ...
elapsed = time.monotonic() - start  # O(1)
```

## Sleeping

```python
import time

# Sleep for at least 0.5 seconds
time.sleep(0.5)  # O(1) time, blocks the thread
```

## Formatting and Parsing

```python
import time

now = time.time()

# Convert to struct_time in UTC or local time
utc = time.gmtime(now)     # O(1)
local = time.localtime(now)  # O(1)

# Format time strings
stamp = time.strftime("%Y-%m-%d %H:%M:%S", local)  # O(n)

# Parse time strings
parsed = time.strptime("2026-01-30 12:34:56", "%Y-%m-%d %H:%M:%S")  # O(n)
```

## Converting Between Timestamps and Tuples

```python
import time

local_tuple = time.localtime()  # O(1)
timestamp = time.mktime(local_tuple)  # O(1)
```

## Related Documentation

- [datetime Module](datetime.md)
- [timeit Module](timeit.md)
