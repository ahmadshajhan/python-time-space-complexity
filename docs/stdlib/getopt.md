# getopt Module

The `getopt` module provides command-line argument parsing using the GNU getopt() style (superseded by argparse but still useful for simple cases).

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `getopt.getopt()` | O(n) | O(n) | n = command-line args |
| Argument parsing | O(n) | O(n) | Parse and store |

## Parsing Command-Line Arguments

### Simple Argument Parsing

```python
import getopt
import sys

# Parse args - O(n) where n = number of args
shortopts = "hv:"  # h=help (no arg), v=verbose (requires arg)
longopts = ["help", "version="]

try:
    opts, args = getopt.getopt(sys.argv[1:], shortopts, longopts)
except getopt.GetoptError as err:
    print(err)
    sys.exit(2)

# Process options - O(n)
for opt, arg in opts:
    if opt in ("-h", "--help"):
        print("Help message")
    elif opt in ("-v", "--version"):
        print(f"Version: {arg}")
```

## Related Documentation

- [argparse Module](argparse.md)
- [sys Module](sys.md)
