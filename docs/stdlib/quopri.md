# quopri Module

The `quopri` module provides encode/decode functions for quoted-printable encoding, used in email and text transmission.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `encodestring()` | O(n) | O(n) | n = input length |
| `decodestring()` | O(n) | O(n) | n = encoded length |

## Encoding and Decoding

### Quoted-Printable Encoding

```python
import quopri

# Encode - O(n)
text = "Hello World! Special: éàü"
encoded = quopri.encodestring(text.encode()).decode()
print(encoded)
# Hello World! Special: =C3=A9=C3=A0=C3=BC

# Decode - O(n)
decoded = quopri.decodestring(encoded.encode()).decode()
print(decoded)  # Hello World! Special: éàü
```

## Related Documentation

- [base64 Module](base64.md)
- [codecs Module](codecs.md)
- [email Module](email.md)
