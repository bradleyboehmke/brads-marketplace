---
title: README Authoring
description: Best practices and templates for generating README sections following standards
tags: [readme, documentation, templates, authoring]
---

# README Authoring Patterns

## Metadata

**Purpose**: Provide 8-section minimal README templates and generation patterns
**Version**: 1.0.0

---

## Instructions

###   Minimal README Structure

The Personal README follows an **8-section minimal structure** with a **link-first approach**:

1. **Project Title & One-Liner** - Name + 1-2 sentence description
2. **Badges Block** *(optional)* - Version, lifecycle, docs, code style
3. **Short Description** - Business problem/solution + core functionality (3-5 sentences)
4. **Installation** - Simple command or link to detailed setup
5. **Documentation** - Links to key resources (architecture, ADRs, guides)
6. **Supporting Components** *(optional)* - Related repos/services
7. **Contributing** - How to contribute or link to CONTRIBUTING.md
8. **Bugs & Enhancements** - Issue tracker link

### Section Generation Reference

| Section | Template | Key Requirements | Common Sources |
|---------|----------|------------------|----------------|
| **1. Title & One-Liner** | `# {Name}`<br>`{1-2 sentence description}` | Project name + what it does | `pyproject.toml`, `package.json`, `setup.py` |
| **2. Badges** *(optional)* | Wrapped in `<!-- badges: start/end -->` comments | MVP/Production tier - see badge options below | Version from metadata, lifecycle from tier, code style from `.pre-commit-config.yaml` |
| **3. Description** | Business problem + solution + functionality (3-5 sentences) | Integrated business context (not separate sections) | `docs/`, code comments, metadata description |
| **4. Installation** | Simple command + optional setup link | Actionable install command | Language-specific: `pip`, `npm`, `cargo` |
| **5. Documentation** | Bulleted list of doc links | Only include links that exist | `docs/quickstart.md`, `docs/architecture.md`, `adr/` |
| **6. Supporting Components** *(optional)* | Dependency list with links | Skip for standalone projects | Docker Compose, K8s configs, related repos |
| **7. Contributing** | Link or inline guidance | Link to CONTRIBUTING.md if exists | `CONTRIBUTING.md`, `docs/contributing.md` |
| **8. Bugs & Enhancements** | Issue tracker link | Clear call-to-action | GitHub Issues from git remote, or prompt user |

**Example (Prototype tier)**:
```markdown
# Customer Churn Predictor

Early-stage prototype for predicting customer churn using transaction history.

## Description

The marketing team needs to identify customers at risk of churning to target retention campaigns effectively. This prototype implements a gradient boosting classifier trained on transaction and engagement data to predict churn probability.

## Installation

\`\`\`bash
pip install -e .
\`\`\`

## Documentation

- See notebooks in `notebooks/` for exploratory analysis
- Model card available in `docs/model-card.md`

## Contributing

This is an experimental prototype. For questions, contact the data science team.

## Bugs & Enhancements

Report issues via [GitHub Issues](https://github.com/USERNAME/churn-predictor/issues).
```

---

### Badge Options Reference

**Standard Personal badge format**:

Badges should be wrapped in HTML comments for maintainability:

```markdown
<!-- badges: start -->
[Badge 1]
[Badge 2]
...
<!-- badges: end -->
```

**Available badge types** (select based on project tier and applicability):

| Badge Type | Example | When to Use | Source |
|------------|---------|-------------|--------|
| **Version/Release** | `[![Releases](https://img.shields.io/badge/released-2.17.0.0-blue.svg)](https://github.com/USERNAME/project/releases)` | All projects with releases | Git tags, `pyproject.toml`, `package.json` |
| **Lifecycle** | `[![Lifecycle](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)` | All tiers (orange=prototype, yellow=mvp, green=production) | Project tier detection |
| **Documentation** | `[![Docs](https://img.shields.io/badge/docs-latest-brightgreen.svg?style=flat)](https://your-project-docs-url/)` | MVP/Production with published docs | Docs URL or relative link |
| **Python Version** | `[![Python version](https://img.shields.io/badge/python-3.12-blue)](https://docs.python.org/3.12/)` | Python projects with version constraint | `pyproject.toml`, `setup.py`, `.python-version` |
| **Code Style: black** | `[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)` | Python projects using black formatter | `.pre-commit-config.yaml`, `pyproject.toml` |
| **Ruff** | `[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)` | Python projects using ruff linter | `.pre-commit-config.yaml`, `pyproject.toml` |
| **Pre-commit** | `[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)` | Projects with pre-commit hooks | `.pre-commit-config.yaml` exists |

**Lifecycle badge color scheme**:
- **Experimental/Prototype**: `orange` - Research, exploratory, not production-ready
- **MVP/Maturing**: `yellow` - Pilot deployment, active development
- **Stable/Production**: `green` - Production-ready, maintained

**Tier-specific badge recommendations**:

| **Tier** | **Recommended Badges** |
|----------|------------------------|
| **Prototype** | Optional: Version, Lifecycle (experimental-orange) |
| **MVP** | Version, Lifecycle (mvp-yellow), Docs |
| **Production** | Version, Lifecycle (stable-green), Docs, Python version (if applicable), Code style, Pre-commit |

**Detection logic**:

```python
# Detect applicable badges from project files
badges = []

# Version/Release (always try to detect)
if has_git_tags or has_version_in_metadata:
    badges.append(("Releases", version_number, releases_url))

# Lifecycle (required for all tiers)
tier = detect_project_tier()  # prototype, mvp, production
lifecycle_colors = {"prototype": "orange", "mvp": "yellow", "production": "green"}
badges.append(("Lifecycle", tier, lifecycle_colors[tier]))

# Documentation (if docs exist)
if docs_url or has_docs_directory:
    badges.append(("Docs", "latest", docs_url))

# Python-specific badges (only for Python projects)
if is_python_project:
    if has_python_version_constraint:
        badges.append(("Python version", python_version, python_docs_url))

    if uses_black_formatter:
        badges.append(("Code style: black", None, black_url))

    if uses_ruff_linter:
        badges.append(("Ruff", None, ruff_badge_url))

# Pre-commit (language-agnostic)
if has_precommit_config:
    badges.append(("pre-commit", "enabled", precommit_url))
```

**Example badge blocks by tier**:

**Prototype tier** (minimal or no badges):
```markdown
<!-- badges: start -->
[![Lifecycle](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
<!-- badges: end -->
```

**MVP tier** (recommended badges):
```markdown
<!-- badges: start -->
[![Version](https://img.shields.io/badge/version-0.2.0-blue.svg)](https://github.com/USERNAME/project/releases)
[![Lifecycle](https://img.shields.io/badge/lifecycle-mvp-yellow.svg)](https://www.tidyverse.org/lifecycle/#maturing)
[![Docs](https://img.shields.io/badge/docs-available-brightgreen.svg?style=flat)](./docs/usage.md)
<!-- badges: end -->
```

**Production tier** (full badge set):
```markdown
<!-- badges: start -->
[![Releases](https://img.shields.io/badge/released-2.17.0.0-blue.svg)](https://github.com/USERNAME/project/releases)
[![Lifecycle](https://img.shields.io/badge/lifecycle-stable-green.svg)](https://www.tidyverse.org/lifecycle/#stable)
[![Docs](https://img.shields.io/badge/docs-latest-brightgreen.svg?style=flat)](https://your-project-docs-url/)
[![Python version](https://img.shields.io/badge/python-3.12-blue)](https://docs.python.org/3.12/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Ruff](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/ruff/main/assets/badge/v2.json)](https://github.com/astral-sh/ruff)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white)](https://github.com/pre-commit/pre-commit)
<!-- badges: end -->
```

**Important notes**:
- Only include badges that are accurate and verifiable
- Don't add Python-specific badges to non-Python projects
- Badge URLs should link to meaningful resources (releases page, docs site, tool documentation)
- Use HTML comment wrappers for easy maintenance

---

### Markdown Formatting Standards

**Heading hierarchy**:
- `#` - Project title only
- `##` - Section headings (Description, Installation, etc.)
- `###` - Subsections (if needed, but keep minimal)

**Code blocks**:
- Always specify language: \`\`\`bash, \`\`\`python, \`\`\`json
- Use for installation commands, API examples

**Links**:
- Relative links for internal docs: `[Setup](docs/setup.md)`
- Absolute links for external resources: `[GitHub Issues](https://github.com/...)`
- Use descriptive link text, not "click here"

**Lists**:
- Use `-` for unordered lists (consistent with   style)
- Use `1.` for ordered lists (auto-numbering)

---

### Context Extraction Patterns

**Python projects** - Read these files in order:
1. `pyproject.toml` - `project.name`, `project.description`, `project.version`
2. `setup.py` - `name`, `description`, `version` if no pyproject.toml
3. `requirements.txt` - Dependencies list
4. Main module docstring - Business context

**JavaScript projects** - Read these files:
1. `package.json` - `name`, `description`, `version`
2. `README.md` - Existing content to preserve
3. Main file docstring - Business context

**Documentation discovery**:
- Architecture: `docs/architecture.md`, `*.drawio`, `*.mmd`
- ADRs: `adr/`, `docs/adr/`
- Setup: `docs/setup.md`, `docs/installation.md`, `INSTALL.md`
- Contributing: `CONTRIBUTING.md`, `docs/contributing.md`

---

## Resources

### Tier-Specific README Example (MVP)

```markdown
# Feature Store API

![Version](https://img.shields.io/badge/version-0.2.0-blue)
![Lifecycle](https://img.shields.io/badge/lifecycle-mvp-yellow)
![Docs](https://img.shields.io/badge/docs-available-green)
![Code Style](https://img.shields.io/badge/code%20style-black-black)

RESTful API for serving customer features to ML models and analytics tools.

## Description

Data scientists need consistent, versioned access to customer features across projects, but currently extract features redundantly from raw data sources. This API provides a centralized feature store with versioning, caching, and real-time serving (<50ms p95).

## Installation

\`\`\`bash
pip install feature-store-client
\`\`\`

For local development, see [Setup Guide](docs/setup.md).

## Documentation

- [Quickstart Guide](docs/quickstart.md) - Get started in 5 minutes
- [API Reference](docs/api.md) - Complete endpoint documentation
- [Architecture](docs/architecture.md) - System design and data flow
- [ADRs](adr/) - Architecture Decision Records

## Supporting Components

- [Feature Pipeline](https://github.com/USERNAME/feature-pipeline) - Batch computation
- [Redis Cluster](internal-link) - Cache layer

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on reporting bugs, submitting changes, and running tests.

## Bugs & Enhancements

Report bugs via [GitHub Issues](https://github.com/USERNAME/feature-store-api/issues).
```

**Tier variations**: Prototype skips badges/components; Production adds comprehensive docs (runbooks, monitoring, deployment guides).

**Business context integration**: See `readme-standards` skill "Before/After Examples" for good/bad business context patterns.

---

### Edge Case Handling

**No project metadata found**:
- Prompt user: "What is the project name?"
- Prompt user: "Provide a one-sentence description"

**No business context found**:
- Prompt user: "What business problem does this solve?"
- Prompt user: "What solution does this project provide?"
- If user unsure: Generate technical description from code analysis

**No documentation exists**:
```markdown
## Documentation

- See inline code documentation and docstrings for implementation details
- Architecture documentation coming soon

For questions, contact [team/person].
```

**No CONTRIBUTING.md**:
- Generate basic contributing section inline (see template above)
- Suggest creating CONTRIBUTING.md for mature projects

**No tests detected**:
- In Contributing section, note: "Please include tests with your contributions"
- Don't specify test command if none exists

---

### Tier-Specific Variations

| **Section** | **Prototype** | **MVP** | **Production** |
|-------------|---------------|---------|----------------|
| **Badges** | Optional (skip) | Include basic badges | Full badge set |
| **Description** | Brief (2-3 sentences) | Moderate (3-4 sentences) | Comprehensive (4-5 sentences) |
| **Documentation Links** | Minimal (notebooks, basic docs) | Moderate (quickstart, API, architecture) | Comprehensive (all resources) |
| **Supporting Components** | Usually none | May have 1-2 dependencies | Multiple service dependencies |
| **Contributing** | Basic inline guidance | Link to CONTRIBUTING.md | Full process documentation |

---

### Link Validation

Before adding links to Documentation section:

1. **Verify file exists**: Use file system check
2. **If missing**: Don't add placeholder link
3. **Suggest creation**: Note in validation report that docs should be created

**Example validation logic**:
```python
docs_to_check = [
    ("Quickstart", "docs/quickstart.md"),
    ("Architecture", "docs/architecture.md"),
    ("ADRs", "adr/"),
]

valid_links = []
for name, path in docs_to_check:
    if file_exists(path):
        valid_links.append((name, path))
```

---

**Remember**: The goal is **minimal, focused READMEs** that serve as clear entry points. Link to detailed documentation rather than embedding everything inline.
