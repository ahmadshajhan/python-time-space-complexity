# curses Module

The `curses` module provides a Python interface to curses, a library for terminal-based GUIs on Unix systems.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `initscr()` | O(1) | O(1) | Initialize terminal |
| Draw operation | O(n) | O(n) | n = pixels/chars |
| Refresh | O(n) | O(n) | Update display |

## Terminal GUI with Curses

### Basic Curses Application

```python
import curses

def main(stdscr):
    # Initialize - O(1)
    curses.curs_set(0)  # Hide cursor
    stdscr.clear()
    
    # Get dimensions - O(1)
    max_y, max_x = stdscr.getmaxyx()
    
    # Draw text - O(n)
    stdscr.addstr(0, 0, "Hello, World!")
    stdscr.addstr(1, 0, f"Terminal: {max_x}x{max_y}")
    
    # Refresh display - O(n)
    stdscr.refresh()
    
    # Wait for input - O(1)
    stdscr.getch()

# Run with curses wrapper - O(1) setup
curses.wrapper(main)
```

## Related Documentation

- [tkinter Module](tkinter.md)
- [turtle Module](turtle.md)
