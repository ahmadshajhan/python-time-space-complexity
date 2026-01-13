# Quick Start Guide

## Initial Setup

### Prerequisites
- Python 3.8+
- pip
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/python-time-space-complexity.git
cd python-time-space-complexity

# Install dependencies
pip install -r requirements.txt
```

## Development

### Serve Documentation Locally

```bash
# Start local server
mkdocs serve

# Open browser to http://localhost:8000
```

### Build Static Site

```bash
# Generate static files
mkdocs build

# Output in site/ directory
# Ready to deploy to GitHub Pages
```

## Project Structure

```
python-time-space-complexity/
├── docs/                      # MkDocs source files
│   ├── index.md              # Landing page
│   ├── builtins/             # Built-in types (list, dict, etc.)
│   ├── stdlib/               # Standard library modules
│   ├── implementations/       # CPython, PyPy, Jython, etc.
│   └── versions/             # Python version guides
├── data/                      # JSON data files
│   ├── builtins.json
│   └── stdlib.json
├── scripts/                   # Utility scripts
│   ├── generate_docs.py      # Generate docs from data
│   └── validate_data.py      # Validate complexity claims
├── .github/workflows/         # GitHub Actions CI/CD
│   └── deploy.yml           # Deploy to GitHub Pages
├── mkdocs.yml               # MkDocs configuration
├── requirements.txt         # Python dependencies
├── README.md                # Project overview
├── LICENSE                  # MIT License
└── CONTRIBUTING.md          # Contribution guidelines
```

## Next Steps

### 1. Configure for Your Domain

Edit `mkdocs.yml`:
```yaml
site_url: https://pythoncomplexity.com  # Your domain
```

Edit `docs/index.md`:
```markdown
Visit the documentation at: [pythoncomplexity.com](https://pythoncomplexity.com)
```

Update GitHub repository link in mkdocs.yml

### 2. Set Up GitHub Pages

In GitHub repository settings:
1. Go to **Settings** → **Pages**
2. Select **Deploy from a branch**
3. Set source to: **gh-pages** branch
4. Save

The workflow will automatically create the gh-pages branch and deploy.

### 3. Configure Domain (Optional)

For custom domain:
1. Update DNS to point to GitHub Pages
2. In GitHub Settings → Pages, enter custom domain
3. Enable HTTPS

### 4. Add Initial Content

- Start with most commonly used operations
- Focus on list, dict, set operations first
- Add stdlib modules (collections, heapq, bisect)
- Document implementation differences
- Add version-specific notes

### 5. Make Your First Commit

```bash
git config user.email "you@example.com"
git config user.name "Your Name"

git add .
git commit -m "Initial commit: Documentation structure and content"
git branch -M main
git remote add origin https://github.com/yourusername/python-time-space-complexity.git
git push -u origin main
```

## Development Workflow

### Adding Documentation

1. Create or edit `.md` file in `docs/`
2. Add link to `mkdocs.yml` navigation
3. Test locally: `mkdocs serve`
4. Commit and push: `git push`
5. GitHub Actions automatically deploys to GitHub Pages

### Adding Data

1. Add structured data to `data/*.json`
2. Update scripts to generate docs if needed
3. Verify with `scripts/validate_data.py`

### Making Changes

```bash
# Create a feature branch
git checkout -b feature/add-numpy-docs

# Make changes
# Test locally
mkdocs serve

# Commit changes
git add .
git commit -m "Add NumPy array complexity analysis"

# Push to GitHub
git push origin feature/add-numpy-docs

# Create Pull Request on GitHub
```

## Maintenance

### Regular Updates

- Check for Python releases
- Add new version documentation
- Update obsolete information
- Fix broken links

### Performance Monitoring

- Track page load times
- Monitor site uptime
- Keep dependencies updated

### Community

- Review and merge pull requests
- Respond to issues
- Welcome contributions
- Maintain code of conduct

## Troubleshooting

### Build Issues

```bash
# Clean and rebuild
rm -rf site/
mkdocs build

# Check for errors
mkdocs serve --verbose
```

### Dependency Issues

```bash
# Reinstall dependencies
pip install --upgrade -r requirements.txt

# Check versions
pip list
```

### GitHub Pages Not Updating

1. Check GitHub Actions tab for errors
2. Verify gh-pages branch exists
3. Check repository settings → Pages
4. Wait ~1-2 minutes for deployment

## Resources

- [MkDocs Documentation](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [Python Documentation](https://docs.python.org/)
- [GitHub Pages Guide](https://pages.github.com/)

## Questions?

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to get help or contribute.
