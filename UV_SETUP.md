# uv Setup & Development Guide

This project uses **[uv](https://github.com/astral-sh/uv)** - a fast, dependency resolver written in Rust. It replaces `pip`, `pip-tools`, and `venv`.

## Why uv?

- **10-100x faster** than traditional pip
- **Single tool** for pip, pip-tools, virtualenv
- **Deterministic** - `uv.lock` for reproducible builds
- **Pythonic** - Drop-in pip replacement
- **Modern** - Built for modern Python workflows

## Installation

### Option 1: Official Installer (Recommended)

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Option 2: Homebrew (macOS/Linux)

```bash
brew install uv
```

### Option 3: From Source (Python)

```bash
pip install uv
```

### Verify Installation

```bash
uv --version
```

## Project Setup

### 1. Initialize Virtual Environment & Install Dependencies

```bash
# One command to set up everything
uv sync

# This will:
# - Create .venv/ virtual environment
# - Install all dependencies from pyproject.toml
# - Install dev dependencies
# - Generate uv.lock
```

### 2. Activate Virtual Environment (Optional)

uv automatically uses the virtual environment, but you can activate it:

```bash
# On Linux/macOS
source .venv/bin/activate

# On Windows
.venv\Scripts\activate
```

### 3. Run Commands

uv automatically manages the virtual environment:

```bash
# Run a command in the virtual environment
uv run mkdocs serve

# Or explicitly invoke Python
uv run python scripts/validate_data.py
```

## Common Development Tasks

### Using Make (Recommended)

```bash
# Install dependencies
make dev

# Serve documentation
make serve

# Build static site
make build

# Check code quality
make check

# Format code
make format

# Run tests
make test

# Clean cache
make clean
```

### Using uv Directly

```bash
# Install/sync dependencies
uv sync

# Install without dev dependencies
uv sync --no-dev

# Add a new dependency
uv add mkdocs-plugin-name

# Add a dev dependency
uv add --dev pytest-plugin-name

# Update all dependencies
uv lock --upgrade

# Run a script
uv run python scripts/generate_docs.py

# Run a command
uv run mkdocs serve
```

## Workflow Examples

### Local Development

```bash
# 1. Set up environment
uv sync

# 2. Start development server
make serve
# or
uv run mkdocs serve

# 3. Make changes to docs/

# 4. Check quality
make lint
# or
uv run ruff check .

# 5. Format code
make format
# or
uv run ruff format .

# 6. Run tests
make test
# or
uv run pytest
```

### Adding Dependencies

```bash
# Add a production dependency
uv add some-package

# Add a development dependency
uv add --dev pytest-plugin

# This automatically:
# - Updates pyproject.toml
# - Updates uv.lock
# - Installs in .venv/
```

### Dependency Management

```bash
# Show installed packages
uv pip list

# Show dependency tree
uv pip show mkdocs --verbose

# Pin specific version
uv add 'mkdocs==1.5.3'

# Update to latest
uv add --upgrade mkdocs

# Remove a package
uv remove mkdocs
```

## Project Configuration

### pyproject.toml Structure

```toml
[project]
name = "python-time-space-complexity"
version = "0.1.0"
requires-python = ">=3.8"
dependencies = [
    "mkdocs>=1.5.0",
    "mkdocs-material>=9.4.0",
    "mkdocs-mermaid2-plugin>=1.1.0",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.4.0",
    "ruff>=0.1.0",
]

[tool.ruff]
line-length = 100

[tool.ruff.lint]
select = ["E", "W", "F", "I", "C", "B", "UP"]

[tool.pytest.ini_options]
testpaths = ["tests"]
```

### Linting & Formatting

```bash
# Check for issues
make lint
# or
uv run ruff check .

# Fix issues
make format
# or
uv run ruff format .
uv run ruff check --fix .
```

### Testing

```bash
# Run all tests
make test
# or
uv run pytest

# Run specific test
uv run pytest tests/test_example.py

# Run with coverage
uv run pytest --cov
```

## CI/CD Integration

### GitHub Actions

The `.github/workflows/deploy.yml` already uses uv:

```yaml
- name: Install dependencies
  run: |
    curl -LsSf https://astral.sh/uv/install.sh | sh
    uv sync
```

### Local Testing Before Push

```bash
# Full quality check before committing
make check

# This runs:
# - Linter (ruff check)
# - Tests (pytest)
```

## Troubleshooting

### Virtual Environment Issues

```bash
# Force recreate virtual environment
rm -rf .venv/
uv sync

# Or
uv venv --force
```

### Dependency Conflicts

```bash
# Clear lock file and regenerate
rm uv.lock
uv lock

# Pin specific versions in pyproject.toml
# [project]
# dependencies = [
#     "mkdocs==1.5.3",  # Pin specific version
# ]
```

### Python Version Issues

```bash
# Check Python version requirement
cat .python-version

# Use specific Python version
uv sync --python 3.11

# List available Python versions
uv python list
```

## Advanced Usage

### Virtual Environment Management

```bash
# Create venv with specific Python
uv venv --python 3.11

# Use different venv location
uv sync --venv /path/to/venv

# List Python versions
uv python list

# Install specific Python version
uv python install 3.12
```

### Dependency Resolution

```bash
# Show dependency tree
uv pip show mkdocs --depth 10

# Check for security vulnerabilities
pip-audit  # Or manually check advisories

# Generate requirements file (for pip compatibility)
uv pip compile pyproject.toml > requirements.txt
```

### Performance Optimization

```bash
# Use offline mode (requires pre-cached packages)
uv sync --offline

# Increase verbosity for debugging
uv sync --verbose

# Show what uv is doing
uv sync --debug
```

## Migration from pip

### Old Way (pip)

```bash
pip install -r requirements.txt
pip install --upgrade package-name
```

### New Way (uv)

```bash
uv sync
uv add package-name@latest
```

### Benefits

| Feature | pip | uv |
|---------|-----|-----|
| Speed | Slow | 10-100x faster |
| Dependency resolution | Basic | Better |
| Lock files | Requires pip-tools | Built-in (uv.lock) |
| Virtual env | Separate tool | Built-in |
| Installation | Multiple tools | Single tool |

## Further Reading

- [uv Documentation](https://docs.astral.sh/uv/)
- [Ruff Documentation](https://docs.astral.sh/ruff/)
- [pyproject.toml Specification](https://packaging.python.org/en/latest/specifications/pyproject-toml/)

## Quick Reference

```bash
# Setup
uv sync                          # Install all deps

# Development
make dev                         # Setup dev environment
make serve                       # Run dev server
make lint                        # Check code
make format                      # Format code
make test                        # Run tests

# Maintenance
uv add package-name              # Add dependency
uv add --dev pytest              # Add dev dependency
uv remove package-name           # Remove dependency
uv lock --upgrade                # Update all dependencies
make clean                       # Clean cache

# Advanced
uv pip list                      # Show packages
uv run python script.py          # Run Python script
uv python list                   # Available Python versions
```

---

**All setup, no complexity. Just `uv sync` and you're ready to go!**
