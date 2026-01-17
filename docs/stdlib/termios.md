# termios Module

The `termios` module provides POSIX-style terminal I/O control on Unix systems, allowing terminal mode configuration.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `tcgetattr()` | O(1) | O(1) | Get settings |
| `tcsetattr()` | O(1) | O(1) | Set settings |

## Terminal Configuration

### Getting and Setting Terminal Modes

```python
import termios
import sys

# Get current settings - O(1)
old_settings = termios.tcgetattr(sys.stdin.fileno())

try:
    # Modify settings
    new_settings = old_settings[:]
    new_settings[3] &= ~termios.ICANON  # Disable canonical mode
    
    # Apply settings - O(1)
    termios.tcsetattr(
        sys.stdin.fileno(),
        termios.TCSADRAIN,
        new_settings
    )
    
    # Now stdin is in raw mode
    ch = sys.stdin.read(1)
    print(f"Got: {repr(ch)}")
    
finally:
    # Restore settings - O(1)
    termios.tcsetattr(
        sys.stdin.fileno(),
        termios.TCSADRAIN,
        old_settings
    )
```

## Related Documentation

- [tty Module](tty.md)
- [pty Module](pty.md)
