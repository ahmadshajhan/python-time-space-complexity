# Tokenize Module

The `tokenize` module provides a lexical analyzer for Python source code, tokenizing it into individual tokens.

## Complexity Reference

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| `generate_tokens(readline)` | O(n) | O(1) | n = source length; generator yields tokens lazily |
| `tokenize(readline)` | O(n) | O(1) | Binary mode tokenization |
| `detect_encoding(readline)` | O(n) | O(1) | n = header size |
| `untokenize(tokens)` | O(n) | O(n) | n = token count |

## Common Operations

### Tokenizing Python Source

```python
import tokenize
import io

# O(n) where n = source length
source = """
x = 1 + 2
print(x)
"""

readline = io.StringIO(source).readline

# O(n) to tokenize entire source
tokens = list(tokenize.generate_tokens(readline))

# Each token: TokenInfo(type, string, start, end, line)
for token in tokens:
    print(f"{token.type} {token.string!r}")
# Output:
# NAME 'x'
# OP '='
# NUMBER '1'
# OP '+'
# NUMBER '2'
# NEWLINE '\n'
# NAME 'print'
# OP '('
# NAME 'x'
# OP ')'
```

### Reading Python Files

```python
import tokenize

# O(n) where n = file size
with open('script.py', 'rb') as f:
    # O(n) to tokenize binary file
    tokens = list(tokenize.tokenize(f.readline))

# Process tokens - O(k) where k = token count
for token in tokens:
    if token.type == tokenize.NAME:
        print(f"Identifier: {token.string}")
    elif token.type == tokenize.STRING:
        print(f"String: {token.string}")
```

## Common Use Cases

### Code Analysis

```python
import tokenize
import io

def analyze_python_code(source):
    """Analyze code structure - O(n)"""
    readline = io.StringIO(source).readline
    
    # O(n) to tokenize where n = source length
    tokens = list(tokenize.generate_tokens(readline))
    
    analysis = {
        'functions': [],
        'variables': [],
        'imports': [],
        'operators': set(),
    }
    
    # O(k) to process tokens where k = token count
    i = 0
    while i < len(tokens):
        token = tokens[i]
        
        # Check for function definition - O(1) per check
        if (token.type == tokenize.NAME and 
            token.string == 'def' and 
            i + 1 < len(tokens)):
            analysis['functions'].append(tokens[i + 1].string)
        
        # Check for operators - O(1)
        elif token.type == tokenize.OP:
            analysis['operators'].add(token.string)
        
        i += 1
    
    return analysis

# Usage - O(n)
code = """
def add(a, b):
    return a + b

x = 10 * 5
"""
result = analyze_python_code(code)
print(result)
```

### Detecting Encoding

```python
import tokenize
import io

def detect_python_encoding(filename):
    """Detect file encoding - O(n)"""
    # O(n) where n = header size (usually small)
    with open(filename, 'rb') as f:
        # Reads only first/second line usually
        try:
            encoding = tokenize.detect_encoding(f.readline)
            return encoding[0]  # Returns encoding name
        except (SyntaxError, UnicodeDecodeError):
            return 'utf-8'  # Fallback

# Usage - O(n) for small header
encoding = detect_python_encoding('script.py')
print(f"Encoding: {encoding}")
```

### Pretty-Printing Source Code

```python
import tokenize
import io

def highlight_tokens(source):
    """Pretty-print with token info - O(n)"""
    readline = io.StringIO(source).readline
    
    # O(n) to tokenize
    tokens = list(tokenize.generate_tokens(readline))
    
    # O(k) to display where k = token count
    for token in tokens:
        token_name = tokenize.tok_name[token.type]
        print(f"{token_name:10} {token.string!r:20} {token.start} -> {token.end}")

# Usage - O(n)
code = "x = 1 + 2"
highlight_tokens(code)
```

### Token Stream Processing

```python
import tokenize
import io

def remove_comments(source):
    """Remove comments from code - O(n)"""
    readline = io.StringIO(source).readline
    
    # O(n) to tokenize where n = source length
    tokens = list(tokenize.generate_tokens(readline))
    
    # O(k) to filter where k = token count
    filtered = [t for t in tokens 
                if t.type != tokenize.COMMENT]
    
    # O(n) to untokenize
    return tokenize.untokenize(filtered)

# Usage - O(n)
code = """
x = 1  # Initialize x
print(x)  # Print value
"""
clean_code = remove_comments(code)
```

### Counting Code Metrics

```python
import tokenize
import io

def count_code_metrics(source):
    """Count various code metrics - O(n)"""
    readline = io.StringIO(source).readline
    
    # O(n) to tokenize
    tokens = list(tokenize.generate_tokens(readline))
    
    metrics = {
        'lines': 0,
        'identifiers': 0,
        'numbers': 0,
        'strings': 0,
        'operators': 0,
        'keywords': 0,
    }
    
    # O(k) to process
    for token in tokens:
        # O(1) per token type check
        if token.type == tokenize.NEWLINE:
            metrics['lines'] += 1
        elif token.type == tokenize.NAME:
            metrics['identifiers'] += 1
        elif token.type == tokenize.NUMBER:
            metrics['numbers'] += 1
        elif token.type == tokenize.STRING:
            metrics['strings'] += 1
        elif token.type == tokenize.OP:
            metrics['operators'] += 1
    
    return metrics

# Usage - O(n)
code = "x = 1 + 2; print('hello')"
metrics = count_code_metrics(code)
print(metrics)
```

## Performance Tips

### Use Generator Form for Large Files

```python
import tokenize

def process_large_file(filename):
    """Process file without loading all tokens - O(1) memory"""
    with open(filename, 'rb') as f:
        # O(n) time but O(1) memory - generator
        for token in tokenize.tokenize(f.readline):
            # Process one token at a time
            if token.type == tokenize.NAME:
                yield token.string

# Usage - O(1) memory for any file size
for identifier in process_large_file('large_script.py'):
    print(identifier)
```

### Cache Tokenized Results

```python
import tokenize
import io

class TokenCache:
    """Cache tokenized code - O(1) lookup"""
    
    def __init__(self):
        self._cache = {}
    
    def get_tokens(self, source):
        """O(1) cached or O(n) new tokenization"""
        source_id = hash(source)
        
        if source_id not in self._cache:
            # O(n) first time where n = source length
            readline = io.StringIO(source).readline
            self._cache[source_id] = list(
                tokenize.generate_tokens(readline)
            )
        
        return self._cache[source_id]

# Usage
cache = TokenCache()
tokens = cache.get_tokens(code)  # O(n)
tokens = cache.get_tokens(code)  # O(1)
```

### Filter Early for Efficiency

```python
import tokenize
import io

# Bad: Tokenize all, then filter - O(n) + O(k)
tokens = list(tokenize.generate_tokens(readline))
identifiers = [t for t in tokens if t.type == tokenize.NAME]

# Good: Filter while tokenizing - O(n)
identifiers = [t for t in tokenize.generate_tokens(readline)
               if t.type == tokenize.NAME]
```

## Token Types

```python
import tokenize

# Main token types:
# NAME - identifiers
# NUMBER - numeric literals
# STRING - string literals
# COMMENT - comments
# OP - operators
# NEWLINE - line breaks
# INDENT/DEDENT - indentation changes
# ERRORTOKEN - syntax errors
# ENDMARKER - end of input
```

## Related Documentation

- [Ast Module](ast.md) - Abstract syntax trees
- [Code Module](code.md) - Code compilation
- [Re Module](re.md) - Regular expressions
