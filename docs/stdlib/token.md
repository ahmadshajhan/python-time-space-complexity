# token Module

The `token` module provides token type constants used by Python's tokenizer, representing different syntax elements like operators, keywords, and literals.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Access token constant | O(1) | O(1) | Module-level constants |
| `tok_name[type]` | O(1) | O(1) | Dict lookup for name |

## Token Type Constants

### Using Token Types

```python
import token
import tokenize
import io

code = "x = 1 + 2"

# Tokenize - O(n)
tokens = tokenize.generate_tokens(io.StringIO(code).readline)

for tok in tokens:
    tok_type, tok_string, start, end, line = tok
    
    # Get token name - O(1)
    tok_name = token.tok_name[tok_type]
    print(f"{tok_name:10} {repr(tok_string)}")

# Output:
# NAME       'x'
# OP         '='
# NUMBER     '1'
# OP         '+'
# NUMBER     '2'
# ENDMARKER  ''
```

## Related Documentation

- [tokenize Module](tokenize.md)
- [keyword Module](keyword.md)
