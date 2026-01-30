# optparse Module

The `optparse` module provides option parsing functionality (deprecated in favor of argparse but still used in legacy code).

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `OptionParser.parse_args()` | O(n) avg, O(n·m) worst | O(n) | n = args, m = long options (abbr matching) |
| Add option | O(1) | O(1) | Register option |

## Parsing Options

### Basic Option Parsing

```python
import optparse

# Create parser - O(1)
parser = optparse.OptionParser()

# Add options - O(1) each
parser.add_option("-f", "--file", dest="filename")
parser.add_option("-v", "--verbose", action="store_true")

# Parse arguments - O(n) average; O(n·m) worst-case with long option abbreviations
(options, args) = parser.parse_args()

print(options.filename)
print(options.verbose)
```

## Related Documentation

- [argparse Module](argparse.md)
- [getopt Module](getopt.md)
