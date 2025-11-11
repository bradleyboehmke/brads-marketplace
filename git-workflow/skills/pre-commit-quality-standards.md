---
title: Pre-Commit Quality Standards
description: Project type detection, quality checks, and pre-commit configurations for pre-commit validation
tags: [pre-commit, quality, linting, security, project-types, validation]
---

# Pre-Commit Quality Standards

## Metadata

**Purpose**: Define project type detection patterns, pre-commit quality checks, and standard pre-commit configurations for different project types
**Applies to**: Pre-commit validation commands and pre-commit setup workflows
**Version**: 1.0.0

---

## Instructions

### Project Type Detection

Use file system indicators to determine project type(s):

#### Python Projects
**Indicators**:
- `pyproject.toml` (modern Python packaging)
- `setup.py` (traditional Python packaging)
- `requirements.txt` or `requirements/*.txt`
- `Pipfile` (pipenv)
- Presence of `*.py` files in src/ or root

**Detection command**:
```bash
ls -la | grep -E 'pyproject.toml|setup.py|requirements.txt|Pipfile'
find . -maxdepth 2 -name "*.py" | head -1
```

#### Data Science Projects
**Indicators**:
- `*.ipynb` Jupyter notebooks
- Common data directories: `data/`, `notebooks/`, `models/`
- Data files: `*.csv`, `*.parquet`, `*.pkl`
- ML config files: `mlflow.yaml`, `dvc.yaml`

**Detection command**:
```bash
find . -name "*.ipynb" | head -1
ls -d data/ notebooks/ models/ 2>/dev/null
```

#### Plugin Marketplace Projects
**Indicators**:
- `.claude-plugin/` directory
- `.claude-plugin/plugin.json` or `.claude-plugin/marketplace.json`
- `commands/`, `skills/`, `agents/` directories

**Detection command**:
```bash
ls -d .claude-plugin/ 2>/dev/null
```

#### Mixed Projects
Projects may have multiple types (e.g., Python + Jupyter, Python + Marketplace). Report all detected types.

### Universal Quality Checks

These checks apply to **all project types**:

#### 1. Commit Message Validation
Reference: `commit-message-standards` skill
- Format: `<type>(<scope>): <subject>`
- Length: Subject ≤50 characters
- Issue linking: Based on commit type

#### 2. Branch Naming Validation
Reference: `github-workflow-patterns` skill
- Format: `<type>/<description>`
- Valid types: feature, fix, hotfix, refactor, docs, experiment, chore
- Lowercase with hyphens

#### 3. Secret Detection
Scan for common secret patterns:
```regex
# API Keys
(api[_-]?key|apikey)[\s:=]["']?[a-zA-Z0-9]{20,}

# AWS Keys
(aws[_-]?access[_-]?key[_-]?id|AKIA[0-9A-Z]{16})

# Private Keys
-----BEGIN (RSA |DSA |EC )?PRIVATE KEY-----

# Tokens
(github[_-]?token|gh[pous]_[a-zA-Z0-9]{36,})
(sk-[a-zA-Z0-9]{48})  # OpenAI/Anthropic

# Passwords
(password|passwd|pwd)[\s:=]["'][^"']{8,}

# Generic secrets
(secret|token)[\s:=]["'][a-zA-Z0-9+/=]{20,}
```

**Check command**:
```bash
git diff --staged | grep -E '(api[_-]?key|password|secret|token|AWS|AKIA|sk-[a-zA-Z0-9])'
```

#### 4. Large File Detection
**Thresholds**:
- Warn: >5MB
- Fail: >10MB (unless using Git LFS)

**Check command**:
```bash
git diff --staged --name-only | python3 -c "
import sys, os
for line in sys.stdin:
    file = line.strip()
    if os.path.isfile(file):
        size = os.path.getsize(file)
        if size > 10*1024*1024:
            print(f'{file}: {size/1024/1024:.2f} MB')
"
```

#### 5. Merge Conflict Markers
```bash
git diff --staged | grep -E '^(<{7}|={7}|>{7})'
```

#### 6. Trailing Whitespace
```bash
git diff --staged --check
```

#### 7. Direct Commits to Protected Branches
```bash
branch=$(git branch --show-current)
if [[ "$branch" == "main" || "$branch" == "master" ]]; then
  echo "ERROR: Direct commits to $branch not allowed"
fi
```

### Project-Specific Quality Checks

#### Python Projects

**Syntax Validation**:
```bash
# Check Python syntax
for file in $(git diff --staged --name-only | grep '\.py$'); do
  python -m py_compile "$file"
done
```

**Common Issues to Detect**:
```bash
# Debug statements
grep -r "import pdb" $(git diff --staged --name-only)
grep -r "breakpoint()" $(git diff --staged --name-only)

# Print debugging (warn only, not fail)
grep -r "print(" $(git diff --staged --name-only | grep '\.py$')

# Hardcoded paths (warn)
grep -E '(/Users/|/home/|C:\\)' $(git diff --staged --name-only | grep '\.py$')
```

**Type Hints** (for production-tier projects):
```bash
# Check if type hints are present
grep -E ': (str|int|float|bool|List|Dict|Optional)' file.py
```

#### Plugin Marketplace Projects

**JSON Validation**:
```bash
# Validate all plugin.json files
for file in $(find . -path "*/.claude-plugin/plugin.json"); do
  python -m json.tool "$file" >/dev/null || echo "Invalid JSON: $file"
done

# Validate marketplace.json
python -m json.tool .claude-plugin/marketplace.json >/dev/null
```

**Markdown Quality**:
```bash
# Check for trailing whitespace
grep -n '\s$' *.md

# Check for proper heading hierarchy
# (H1 only once, H2-H6 properly nested)
```

**Plugin Structure Validation**:
- Required files: `.claude-plugin/plugin.json`
- Required fields in plugin.json: name, description, version, author
- Commands must have YAML frontmatter with description
- Skills should follow 3-tier structure (Metadata/Instructions/Resources)

#### Data Science Projects

**Notebook Checks**:
```bash
# Large notebooks (>5MB)
find . -name "*.ipynb" -size +5M

# Check for outputs in notebooks (optional - some teams want outputs cleared)
grep -l '"outputs": \[' *.ipynb | grep -v '"outputs": \[\]'

# Check for execution count in notebooks
grep -l '"execution_count":' *.ipynb
```

**Data File Checks**:
```bash
# Large data files that shouldn't be in git
find data/ -type f -size +10M 2>/dev/null

# Check if Git LFS is configured for data files
git lfs ls-files | grep -E '\.(csv|parquet|pkl|h5)$'
```

**Model File Checks**:
```bash
# Large model files
find models/ -type f -size +100M 2>/dev/null
```

---

## Resources

### Pre-Commit Configuration Templates

#### Python Project Template

```yaml
# .pre-commit-config.yaml for Python projects
repos:
  # Code formatting
  - repo: https://github.com/psf/black
    rev: 23.12.1
    hooks:
      - id: black
        language_version: python3.11

  # Linting
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.1.9
    hooks:
      - id: ruff
        args: [--fix, --exit-non-zero-on-fix]

  # Type checking
  - repo: https://github.com/pre-commit/mirrors-mypy
    rev: v1.8.0
    hooks:
      - id: mypy
        additional_dependencies: [types-all]

  # Security and general checks
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-json
      - id: check-added-large-files
        args: ['--maxkb=10000']
      - id: check-merge-conflict
      - id: detect-private-key

  # Secret detection
  - repo: https://github.com/Yelp/detect-secrets
    rev: v1.4.0
    hooks:
      - id: detect-secrets
        args: ['--baseline', '.secrets.baseline']
```

#### Plugin Marketplace Project Template

```yaml
# .pre-commit-config.yaml for Plugin Marketplace projects
repos:
  # Markdown linting
  - repo: https://github.com/igorshubovych/markdownlint-cli
    rev: v0.38.0
    hooks:
      - id: markdownlint
        args: [--fix]

  # YAML validation
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: check-yaml
      - id: check-json
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-merge-conflict

  # JSON formatting
  - repo: https://github.com/pre-commit/mirrors-prettier
    rev: v3.1.0
    hooks:
      - id: prettier
        types_or: [json, yaml, markdown]
```

#### Data Science Project Template

```yaml
# .pre-commit-config.yaml for Data Science projects
repos:
  # Python formatting and linting (same as Python template)
  - repo: https://github.com/psf/black
    rev: 23.12.1
    hooks:
      - id: black

  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.1.9
    hooks:
      - id: ruff

  # Jupyter notebook handling
  - repo: https://github.com/nbQA-dev/nbQA
    rev: 1.7.1
    hooks:
      - id: nbqa-black
      - id: nbqa-ruff

  # Clear notebook outputs
  - repo: https://github.com/kynan/nbstripout
    rev: 0.6.1
    hooks:
      - id: nbstripout

  # General checks
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-added-large-files
        args: ['--maxkb=5000']
      - id: detect-private-key
```

### Secret Detection Patterns Reference

**High-confidence patterns** (should fail):
- AWS Access Key: `AKIA[0-9A-Z]{16}`
- GitHub Personal Access Token: `ghp_[a-zA-Z0-9]{36}`
- GitHub OAuth Token: `gho_[a-zA-Z0-9]{36}`
- Private Key: `-----BEGIN.*PRIVATE KEY-----`
- Anthropic/OpenAI Key: `sk-[a-zA-Z0-9]{48}`

**Medium-confidence patterns** (should warn):
- Generic API key assignment: `api_key\s*=\s*["'][^"']+["']`
- Password assignment: `password\s*=\s*["'][^"']+["']`
- Token assignment: `token\s*=\s*["'][^"']+["']`

**Low-confidence patterns** (informational only):
- Environment variable usage: `os.getenv('API_KEY')`
- Config references: `config['secret']`

### Quality Check Severity Levels

**FAIL (Blocking)**:
- Secrets detected (high confidence)
- Syntax errors
- Merge conflict markers
- Direct commits to main/master
- Files >10MB without Git LFS

**WARN (Non-blocking)**:
- Print statements in Python code
- Files >5MB
- Debug statements in non-test files
- Missing type hints (production tier only)
- Secrets detected (medium confidence)

**INFO (Informational)**:
- Pre-commit not configured
- Optional checks not run
- Secrets detected (low confidence)
