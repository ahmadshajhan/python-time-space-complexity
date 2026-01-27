# gc Module

The `gc` module provides access to the garbage collector for tracking and controlling cyclic
references in Python.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `enable()` | O(1) | O(1) | Enable cyclic GC |
| `disable()` | O(1) | O(1) | Disable cyclic GC |
| `isenabled()` | O(1) | O(1) | Check GC status |
| `collect()` | O(n) | O(n) | n = tracked objects |
| `set_threshold()` | O(1) | O(1) | Update generation thresholds |
| `get_threshold()` | O(1) | O(1) | Read thresholds |
| `get_count()` | O(1) | O(1) | Generation allocation counts |
| `get_stats()` | O(1) | O(1) | GC stats per generation |
| `set_debug()` | O(1) | O(1) | Set debug flags |
| `get_debug()` | O(1) | O(1) | Read debug flags |
| `get_objects()` | O(n) | O(n) | Return tracked objects |
| `get_referrers()` | O(n) | O(n) | Find objects referring to targets |
| `get_referents()` | O(n) | O(n) | Find objects referenced by targets |
| `is_tracked()` | O(1) | O(1) | Check GC tracking |
| `is_finalized()` | O(1) | O(1) | Check finalization state |
| `freeze()` | O(n) | O(n) | Freeze tracked objects |
| `unfreeze()` | O(n) | O(n) | Unfreeze tracked objects |
| `get_freeze_count()` | O(1) | O(1) | Count frozen objects |

## Common Operations

### Trigger Collection

```python
import gc

# Force collection - O(n)
collected = gc.collect()
print(collected)
```

### Enable or Disable GC

```python
import gc

# Disable cyclic GC - O(1)
gc.disable()

# Enable cyclic GC - O(1)
gc.enable()

# Check state - O(1)
if gc.isenabled():
    print("GC enabled")
```

### Inspect Thresholds and Counters

```python
import gc

thresholds = gc.get_threshold()  # O(1)
counts = gc.get_count()          # O(1)
```

### Reference Inspection

```python
import gc

obj = []
referrers = gc.get_referrers(obj)  # O(n)
referents = gc.get_referents(obj)  # O(n)
```

## Debugging Flags

Common flags include:

- `DEBUG_STATS`
- `DEBUG_COLLECTABLE`
- `DEBUG_UNCOLLECTABLE`
- `DEBUG_SAVEALL`
- `DEBUG_LEAK`

## Related Documentation

- [sys Module](sys.md)
- [weakref Module](weakref.md)
