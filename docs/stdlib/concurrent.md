# concurrent Module

The `concurrent` module provides high-level interfaces for asynchronous execution with threads or processes through Executors and Futures.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Executor setup | O(1) | O(n) | n = workers |
| Submit task | O(1) | O(1) | Queue work |
| Wait for results | O(n) | O(n) | n = tasks |

## Thread and Process Pools

### ThreadPoolExecutor

```python
from concurrent.futures import ThreadPoolExecutor
import time

def task(name, duration):
    time.sleep(duration)
    return f"{name} done"

# Create executor - O(1)
with ThreadPoolExecutor(max_workers=3) as executor:
    # Submit tasks - O(1) each
    futures = [
        executor.submit(task, f"Task{i}", i)
        for i in range(5)
    ]
    
    # Wait for all - O(n)
    results = [f.result() for f in futures]
    print(results)
```

### ProcessPoolExecutor

```python
from concurrent.futures import ProcessPoolExecutor

def cpu_task(n):
    return sum(i*i for i in range(n))

# Create executor - O(1)
with ProcessPoolExecutor(max_workers=4) as executor:
    # Submit - O(1) each
    futures = [
        executor.submit(cpu_task, 10**6 + i)
        for i in range(4)
    ]
    
    # Get results - O(n)
    results = [f.result() for f in futures]
```

## Related Documentation

- [threading Module](threading.md)
- [multiprocessing Module](multiprocessing.md)
- [asyncio Module](asyncio.md)
