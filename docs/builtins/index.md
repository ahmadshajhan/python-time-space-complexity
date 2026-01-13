# Built-in Types Complexity

Python's built-in types have well-defined complexity characteristics for their operations. This section provides detailed analysis for the most commonly used types.

## Overview

| Type | Use Case | Avg Access | Avg Insert | Avg Delete |
|------|----------|-----------|-----------|-----------|
| `list` | Ordered sequences | O(1) | O(n) | O(n) |
| `dict` | Key-value mapping | O(1) | O(1) | O(1) |
| `set` | Unique items | - | O(1) | O(1) |
| `tuple` | Immutable sequence | O(1) | - | - |
| `str` | Text | O(1) | - | - |

## Detailed Guides

- **[List](list.md)** - Most flexible sequence type
- **[Dictionary](dict.md)** - Hash-based key-value storage
- **[Set](set.md)** - Unordered unique items
- **[Tuple](tuple.md)** - Immutable sequences
- **[String](str.md)** - Text and character sequences

## Key Concepts

### Amortized Complexity

Some operations like `list.append()` have **amortized O(1)** complexity. This means:
- Most append operations are O(1)
- Occasionally, a resize happens requiring O(n)
- Over many operations, the average is O(1)

### Implementation Details

CPython uses:
- **Lists**: Dynamic arrays with over-allocation
- **Dicts**: Hash tables with open addressing (Python 3.6+)
- **Sets**: Hash tables (similar to dicts)

## Version Notes

Different Python versions have optimizations:

- **Python 3.6+**: Dict insertion order guaranteed
- **Python 3.9+**: New dict implementation improvements
- **Python 3.10+**: Additional optimizations for common operations

See [Versions](../versions/index.md) for detailed changelog by release.
