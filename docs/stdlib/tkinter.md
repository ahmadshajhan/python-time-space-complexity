# tkinter Module

The `tkinter` module provides Python bindings to Tk, a popular GUI toolkit for creating graphical user interfaces.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Create widget | O(1) | O(1) | Initialize component; Tk call overhead |
| Draw GUI | O(n) | O(n) | n = widgets; rendering cost is OS-dependent |
| Event handling | O(1) | O(1) | Per event dispatch; handler complexity varies |

## Building GUI Applications

### Simple Tkinter Window

```python
import tkinter as tk

# Create window - O(1)
root = tk.Tk()
root.title("My App")
root.geometry("400x300")

# Create widgets - O(1) each
label = tk.Label(root, text="Hello, Tkinter!")
label.pack()

button = tk.Button(root, text="Click Me")
button.pack()

# Handle events - O(1)
def on_click():
    label.config(text="Button clicked!")

button.config(command=on_click)

# Run event loop - O(e) where e = events processed
root.mainloop()
```

### Layouts and Widgets

```python
import tkinter as tk

root = tk.Tk()

# Frame layout - O(1)
frame = tk.Frame(root)
frame.pack(fill=tk.BOTH, expand=True)

# Add widgets - O(n)
tk.Label(frame, text="Name:").grid(row=0, column=0)
entry = tk.Entry(frame)
entry.grid(row=0, column=1)

tk.Label(frame, text="Message:").grid(row=1, column=0)
text = tk.Text(frame, height=4, width=30)
text.grid(row=1, column=1)

root.mainloop()
```

## Related Documentation

- [turtle Module](turtle.md)
- [curses Module](curses.md)
