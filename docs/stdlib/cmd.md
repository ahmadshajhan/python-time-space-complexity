# cmd Module

The `cmd` module provides a framework for building line-oriented interactive command interpreters.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `Cmd()` init | O(1) | O(1) | Create interpreter |
| Parse command | O(n) | O(n) | n = input length |
| Command dispatch | O(1) | O(1) | Call handler |
| `IDENTCHARS` | O(1) | O(1) | Identifier character set |
| `PROMPT` | O(1) | O(1) | Default prompt string |

## Building Interactive Shells

### Simple Command Interpreter

```python
import cmd

class MyShell(cmd.Cmd):
    """Simple command interpreter"""
    
    prompt = "myshell> "
    
    def do_hello(self, arg):
        """Say hello"""
        print(f"Hello {arg}!")
    
    def do_exit(self, arg):
        """Exit shell"""
        return True

# Run shell - O(m)
shell = MyShell()
shell.cmdloop()

# User can type:
# hello world
# exit
```

### Advanced Commands

```python
import cmd

class AdvancedShell(cmd.Cmd):
    def do_add(self, arg):
        """Add two numbers: add 3 5"""
        try:
            parts = arg.split()
            result = int(parts[0]) + int(parts[1])
            print(f"Result: {result}")
        except (ValueError, IndexError):
            print("Usage: add <int> <int>")
    
    def help_add(self):
        print("Add two integers together")

shell = AdvancedShell()
shell.onecmd("add 10 20")  # Result: 30
```

## Related Documentation

- [code Module](code.md)
- [readline Module](readline.md)
