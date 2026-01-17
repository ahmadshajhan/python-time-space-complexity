# tty Module

The `tty` module provides functions for working with terminal I/O control on Unix systems, setting raw and cooked modes.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `setraw()` / `setcbreak()` | O(1) | O(1) | Configure terminal |
| Restore mode | O(1) | O(1) | Save/restore settings |

## Terminal Mode Control

### Setting Raw Mode

```python
import tty
import sys
import termios

# Save terminal settings
old_settings = termios.tcgetattr(sys.stdin)

try:
    # Set raw mode - O(1)
    tty.setraw(sys.stdin.fileno())
    
    # Now terminal reads character-by-character
    ch = sys.stdin.read(1)
    print(f"Got: {repr(ch)}")
    
finally:
    # Restore - O(1)
    termios.tcsetattr(sys.stdin, termios.TCSADRAIN, old_settings)
```

### Setting Cbreak Mode

```python
import tty
import sys
import termios

old_settings = termios.tcgetattr(sys.stdin)

try:
    # Set cbreak mode - O(1)
    tty.setcbreak(sys.stdin.fileno())
    
    # Read without echo
    ch = sys.stdin.read(1)
    print(f"Pressed: {repr(ch)}")
    
finally:
    termios.tcsetattr(sys.stdin, termios.TCSADRAIN, old_settings)
```

## Related Documentation

- [termios Module](termios.md)
- [pty Module](pty.md)
