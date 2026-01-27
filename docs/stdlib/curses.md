# curses Module

The `curses` module provides a Python interface to curses, a library for terminal-based GUIs on Unix systems.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `initscr()` | O(1) | O(1) | Initialize terminal |
| Draw operation | O(n) | O(n) | n = pixels/chars |
| Refresh | O(n) | O(n) | Update display |
| `newwin()` / `newpad()` | O(1) | O(1) | Create window/pad |
| `endwin()` | O(1) | O(1) | Restore terminal |
| `wrapper()` | O(1) | O(1) | Initialize and cleanup |
| `assume_default_colors()` | O(1) | O(1) | Color defaults |
| `baudrate()` | O(1) | O(1) | Terminal baud rate |
| `beep()` / `flash()` | O(1) | O(1) | Audible/visual alert |
| `can_change_color()` | O(1) | O(1) | Color capability |
| `cbreak()` / `nocbreak()` | O(1) | O(1) | Cbreak mode |
| `echo()` / `noecho()` | O(1) | O(1) | Echo input |
| `nl()` / `nonl()` | O(1) | O(1) | Newline translation |
| `raw()` / `noraw()` | O(1) | O(1) | Raw mode |
| `qiflush()` / `noqiflush()` | O(1) | O(1) | Flush on interrupt |
| `intrflush()` | O(1) | O(1) | Flush input on interrupt |
| `halfdelay()` | O(1) | O(1) | Cbreak with timeout |
| `napms(ms)` | O(1) | O(1) | Sleep in ms |
| `delay_output(ms)` | O(1) | O(1) | Delay output |
| `typeahead(fd)` | O(1) | O(1) | Control typeahead |
| `meta(win, flag)` | O(1) | O(1) | Meta key handling |
| `keyname(ch)` / `unctrl(ch)` | O(1) | O(1) | Key name/printable |
| `killchar()` / `erasechar()` | O(1) | O(1) | Kill/erase char |
| `get_escdelay()` / `set_escdelay()` | O(1) | O(1) | Escape delay |
| `get_tabsize()` / `set_tabsize()` | O(1) | O(1) | Tab size |
| `has_key(code)` | O(1) | O(1) | Key capability |
| `has_colors()` | O(1) | O(1) | Color support |
| `has_extended_color_support()` | O(1) | O(1) | Extended colors |
| `has_ic()` / `has_il()` | O(1) | O(1) | Insert char/line |
| `init_color()` / `color_content()` | O(1) | O(1) | Color definitions |
| `init_pair()` / `pair_content()` | O(1) | O(1) | Color pairs |
| `pair_number()` / `color_pair()` | O(1) | O(1) | Pair lookup |
| `start_color()` / `use_default_colors()` | O(1) | O(1) | Color init/defaults |
| `mousemask()` / `mouseinterval()` | O(1) | O(1) | Mouse config |
| `getmouse()` / `ungetmouse()` | O(1) | O(1) | Mouse events |
| `resize_term()` / `resizeterm()` | O(1) | O(1) | Resize terminal |
| `is_term_resized()` | O(1) | O(1) | Resize check |
| `update_lines_cols()` | O(1) | O(1) | Update size globals |
| `longname()` | O(1) | O(1) | Terminal name |
| `termname()` | O(1) | O(1) | Terminal name bytes |
| `termattrs()` | O(1) | O(1) | Terminal attributes |
| `tigetflag()` / `tigetnum()` / `tigetstr()` | O(1) | O(1) | Terminfo queries |
| `tparm()` | O(1) | O(1) | Terminfo parameterization |
| `setupterm()` | O(1) | O(1) | Initialize terminfo |
| `putp()` | O(n) | O(1) | n = string length |
| `def_prog_mode()` / `def_shell_mode()` | O(1) | O(1) | Save modes |
| `reset_prog_mode()` / `reset_shell_mode()` | O(1) | O(1) | Restore modes |
| `savetty()` / `resetty()` | O(1) | O(1) | Save/restore tty |
| `getsyx()` / `setsyx()` | O(1) | O(1) | Get/set cursor |
| `doupdate()` | O(n) | O(n) | Refresh all windows |
| `getwin()` | O(n) | O(n) | Read window from file |
| `window` | O(1) | O(1) | Window type constructor |
| `ungetch()` / `unget_wch()` | O(1) | O(1) | Push key back |
| `filter()` | O(1) | O(1) | Use stdscr only |

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
