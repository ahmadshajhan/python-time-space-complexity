# opcode Module

The `opcode` module provides access to Python's bytecode opcodes and their properties, useful for bytecode analysis and manipulation.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| Access opcode | O(1) | O(1) | Hash lookup |
| Get opcode info | O(1) | O(1) | Static data |

## Bytecode Opcode Information

### Accessing Opcodes

```python
import opcode

# Get opcode number - O(1)
print(opcode.opmap['LOAD_CONST'])  # 100
print(opcode.opmap['RETURN_VALUE']) # 83

# Get opcode name - O(1)
print(opcode.opname[100])  # 'LOAD_CONST'

# Check if opcode has argument - O(1)
print(opcode.HAVE_ARGUMENT)  # Codes >= 90 have args

# Compare opcodes - O(1)
if opcode.opmap['STORE_NAME'] > opcode.HAVE_ARGUMENT:
    print("Has argument")
```

## Related Documentation

- [dis Module](dis.md)
- [sys Module](sys.md)
