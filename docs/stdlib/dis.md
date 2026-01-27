# dis Module

The `dis` module provides tools to disassemble Python bytecode. It shows the low-level instructions that Python code compiles to.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `dis.dis()` | O(n) | O(n) | n = bytecode instructions |
| `dis.get_instructions()` | O(n) | O(n) | Iterate bytecode |
| Bytecode analysis | O(n) | O(1) | Single pass |
| `dis.Bytecode()` | O(1) | O(1) | Create Bytecode wrapper |
| `dis.code_info()` | O(n) | O(n) | Format code object metadata |
| `dis.show_code()` | O(n) | O(n) | Print code metadata |
| `dis.stack_effect()` | O(1) | O(1) | Stack effect for opcode |
| `dis.findlinestarts()` | O(n) | O(n) | Map bytecode to lines |
| `dis.findlabels()` | O(n) | O(n) | Find jump targets |
| `dis.pretty_flags()` | O(n) | O(n) | Format compiler flags |
| `dis.get_executor()` | O(1) | O(1) | Return current executor |
| `dis.print_instructions()` | O(n) | O(n) | Print Instruction list |
| `dis.disassemble()` | O(n) | O(n) | Disassemble code object |
| `dis.disco()` / `dis.distb()` | O(n) | O(n) | Disassemble object/traceback |
| `dis.main()` | O(n) | O(n) | CLI entrypoint |
| `Instruction` / `Positions` | O(1) | O(1) | Named tuple types |

## Disassembling Functions

### Basic Disassembly

```python
import dis

def add(x, y):
    return x + y

# Disassemble function - O(n)
dis.dis(add)

# Output:
#   2           0 LOAD_FAST                0 (x)
#               2 LOAD_FAST                1 (y)
#               4 BINARY_ADD
#               6 RETURN_VALUE
```

### Analyzing Bytecode Instructions

```python
import dis

def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)

# Get instructions - O(n)
for instr in dis.get_instructions(factorial):
    print(f"{instr.opname:15} {instr.argval}")

# Output shows: LOAD_FAST, LOAD_CONST, COMPARE_OP, etc.
```

## Performance Analysis

### Compare Function Implementations

```python
import dis

def loop_append(n):
    result = []
    for i in range(n):
        result.append(i)
    return result

def list_comp(n):
    return [i for i in range(n)]

print("Loop with append:")
dis.dis(loop_append)

print("\nList comprehension:")
dis.dis(list_comp)
# List comprehension has fewer instructions
```

## Related Documentation

- [ast Module](ast.md)
- [inspect Module](inspect.md)
