# readline Module

The `readline` module provides line-editing support for Python's interactive interpreter, enabling command history and auto-completion.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Setup | O(1) | O(1) | Configure readline |
| Read line | O(n) | O(n) | n = input length |

## Interactive Line Editing

### Using Readline

```python
import readline

# Set up completion - O(1)
def completer(text, state):
    options = ['apple', 'apricot', 'banana']
    matches = [opt for opt in options if opt.startswith(text)]
    
    if state < len(matches):
        return matches[state]
    else:
        return None

readline.set_completer(completer)

# Parse bindings - O(1)
readline.parse_and_bind('tab: complete')

# In interactive mode, user can:
# >>> inp = input("Enter: ")  # Has history and completion
```

### History Management

```python
import readline

# Read history - O(n)
readline.read_history_file('.python_history')

# Add to history - O(1)
readline.add_history('print("test")')

# Save history - O(n)
readline.write_history_file('.python_history')
```

## Related Documentation

- [code Module](code.md)
- [rlcompleter Module](rlcompleter.md)
