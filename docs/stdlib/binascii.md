# binascii Module

The `binascii` module contains functions for converting between binary and ASCII representations, including hex encoding and uuencoding.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `hexlify()` | O(n) | O(n) | n = input length |
| `unhexlify()` | O(n) | O(n) | n = hex length |
| `b2a_base64()` | O(n) | O(n) | Encode to base64 |
| `a2b_base64()` | O(n) | O(n) | Decode base64 |
| `b2a_hex()` / `a2b_hex()` | O(n) | O(n) | Hex encode/decode aliases |
| `b2a_qp()` / `a2b_qp()` | O(n) | O(n) | Quoted-printable encode/decode |
| `b2a_uu()` / `a2b_uu()` | O(n) | O(n) | UUencode/decode |
| `crc32()` | O(n) | O(1) | n = input length |
| `crc_hqx()` | O(n) | O(1) | n = input length |
| `Error` / `Incomplete` | O(1) | O(1) | Exception types |

## Binary-ASCII Conversions

### Hex Encoding

```python
import binascii

# Hex encode - O(n)
data = b'hello'
hex_str = binascii.hexlify(data)
print(hex_str)  # b'68656c6c6f'

# Hex decode - O(n)
decoded = binascii.unhexlify(hex_str)
print(decoded)  # b'hello'
```

### Base64 Encoding

```python
import binascii

# Encode - O(n)
data = b'binary data'
b64 = binascii.b2a_base64(data)
print(b64)

# Decode - O(n)
decoded = binascii.a2b_base64(b64)
print(decoded)
```

## Related Documentation

- [base64 Module](base64.md)
- [uu Module](uu.md)
