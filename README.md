# Python Time & Space Complexity

A comprehensive resource documenting the time and space complexity of Python's built-in functions and standard library operations across different Python versions and implementations.

## Overview

This project provides detailed documentation of algorithmic complexity for:
- **Python Built-ins**: `list`, `dict`, `set`, `str`, etc.
- **Standard Library Modules**: `collections`, `heapq`, `bisect`, and more
- **Multiple Python Versions**: CPython 3.8+
- **Alternative Implementations**: CPython, PyPy, Jython, IronPython

## Features

- 📊 Comprehensive complexity tables for all major built-in types and operations
- 🔄 Version-specific behavior and optimization changes
- 🚀 Implementation-specific notes (CPython vs PyPy vs others)
- 🔍 Interactive search and filtering
- 📱 Mobile-friendly responsive design

## Website

Visit the documentation at: [pythoncomplexity.com](https://pythoncomplexity.com)

## Repository Structure

```
├── docs/                      # MkDocs documentation source
│   ├── index.md              # Landing page
│   ├── builtins/             # Built-in types and functions
│   ├── stdlib/               # Standard library modules
│   ├── implementations/       # Python implementation details
│   └── versions/             # Version-specific guides
├── data/                      # Data files and specs
│   ├── builtins.json         # Built-in operations data
│   └── stdlib.json           # Standard library data
├── scripts/                   # Data generation and processing
│   ├── generate_docs.py      # Generate documentation
│   └── validate_data.py      # Validate complexity data
├── mkdocs.yml               # MkDocs configuration
├── .github/
│   └── workflows/
│       └── deploy.yml       # GitHub Pages deployment
└── requirements.txt         # Python dependencies
```

## Getting Started

### Local Development

```bash
# Install dependencies
pip install -r requirements.txt

# Serve documentation locally
mkdocs serve

# Open browser to http://localhost:8000
```

### Building

```bash
# Build static site
mkdocs build

# Output goes to site/ directory
```

## Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Sources & References

- [Python Official Documentation](https://docs.python.org/3/)
- [TimeComplexity Wiki](https://wiki.python.org/moin/TimeComplexity)
- [Python Enhancement Proposals (PEPs)](https://www.python.org/dev/peps/)
- Implementation source code repositories

## License

MIT License - See [LICENSE](LICENSE) for details

## Disclaimer

While we strive for accuracy, complexity information may vary based on specific implementations and versions. Always verify with official documentation and benchmarks for performance-critical code.
