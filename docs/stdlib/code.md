# code Module

The `code` module provides utilities for evaluating Python code and creating interactive interpreters.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `InteractiveInterpreter()` | O(1) | O(n) | n = namespace vars |
| Execute code | O(n) | O(n) | n = code complexity |
| `InteractiveConsole()` | O(1) | O(n) | n = namespace vars |
| `CommandCompiler()` | O(1) | O(1) | Compiler helper |
| `compile_command()` | O(n) | O(n) | n = input length |
| `interact()` | O(m) | O(n) | m = input lines |
| `Quitter` | O(1) | O(1) | Exit helper |

## Interactive Code Execution

### Running Code Interactively

```python
import code
import sys

# Create interpreter - O(1)
locals_dict = {'x': 10}
interp = code.InteractiveInterpreter(locals_dict)

# Execute code - O(n)
interp.runsource('y = x + 5')
interp.runsource('print(y)')  # 15

# Start REPL - O(m)
interp.interact(banner='Custom REPL')
```

### Interactive Console

```python
import code

# Create console - O(1)
console = code.InteractiveConsole({'x': 42})

# Run commands - O(n)
console.push('result = x * 2')
console.push('print(result)')

# Start interaction - O(m)
console.interact()
```

## Related Documentation

- [codeop Module](codeop.md)
- [ast Module](ast.md)
