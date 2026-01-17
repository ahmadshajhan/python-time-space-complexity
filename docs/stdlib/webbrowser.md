# webbrowser Module

The `webbrowser` module provides a browser control interface, allowing Python programs to open URLs in web browsers.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `open()` | O(1) | O(1) | Launch browser; async system call |
| Open URL | O(1) | O(1) | System call; returns before page loads |

## Opening URLs

### Basic URL Opening

```python
import webbrowser

# Open in default browser - O(1)
webbrowser.open('https://www.example.com')

# Open in new window - O(1)
webbrowser.open_new('https://www.example.com')

# Open in new tab - O(1)
webbrowser.open_new_tab('https://www.example.com')
```

### Specifying Browser

```python
import webbrowser

# Register custom browser - O(1)
chrome = webbrowser.BackgroundBrowser('/usr/bin/google-chrome')

# Open with specific browser - O(1)
chrome.open('https://www.example.com')
```

## Related Documentation

- [urllib Module](urllib.md)
- [subprocess Module](subprocess.md)
