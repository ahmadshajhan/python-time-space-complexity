# gettext Module

The `gettext` module provides internationalization (i18n) support for Python applications through message translation.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `gettext.install()` | O(n) | O(n) | Load translations |
| `translation()` | O(n) | O(n) | Load translation catalog |
| `find()` | O(n) | O(1) | Locate translation file |
| `bindtextdomain()` | O(1) | O(1) | Set global locale dir |
| `textdomain()` | O(1) | O(1) | Set default domain |
| Message lookup | O(1) | O(1) | Hash-based dict |
| `ngettext()` | O(1) | O(1) | Plural form selection |

## Basic Translation

### Installing Gettext

```python
import gettext

# Install translation - O(n)
gettext.install('myapp')

# Now use _() for translatable strings
message = _("Hello, World!")
```

### Loading Translation Files

```python
import gettext

# Load specific translation - O(n)
es = gettext.translation(
    'myapp',  # domain
    localedir='locale',
    languages=['es']
)
es.install()

# Translated strings use _()
print(_("Hello"))  # Hola
```

## Related Documentation

- [locale Module](locale.md)
- [codecs Module](codecs.md)
