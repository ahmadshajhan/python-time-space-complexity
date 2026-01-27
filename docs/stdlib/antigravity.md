# antigravity Module

The `antigravity` module is an Easter egg in Python that opens a web browser to an XKCD comic when imported.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Import module | O(1) | O(1) | Open browser |
| `geohash()` | O(n) | O(1) | n = input length, hashes and encodes |

## The Easter Egg

### Importing antigravity

```python
import antigravity

# Opens: https://xkcd.com/353/
# Shows "Python" comic where person achieves flight
```

## Related Documentation

- [this Module](this.md)
- [webbrowser Module](webbrowser.md)
