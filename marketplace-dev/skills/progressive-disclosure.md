---
title: Progressive Disclosure Pattern
description: Three-tier knowledge loading for efficient token usage
tags: [skills, optimization, token-efficiency, loading-strategy]
---

# Progressive Disclosure Pattern

## Metadata

**Purpose**: Optimize token usage through progressive skill loading
**Pattern**: Three-tier activation (metadata → instructions → resources)
**Benefit**: Load only what's needed when it's needed

---

## Instructions

### The Three-Tier Pattern

Skills should be structured in three distinct sections that load progressively:

#### Tier 1: Metadata (Always Loaded)
**When**: Plugin loads, skill file scanned
**Purpose**: Identification and discovery
**Token Cost**: ~50-100 tokens
**Contains**:
- Title
- Description (1-2 sentences)
- Tags for categorization
- Version/applicability info

**Example**:
```markdown
---
title: Python Packaging Standards
description: Modern Python packaging best practices using pyproject.toml
tags: [python, packaging, standards]
---

# Python Packaging Standards

## Metadata
**Purpose**: Guide Python package structure and configuration
**Applies to**: All Python projects
**Version**: 1.0.0
```

#### Tier 2: Instructions (Loaded When Activated)
**When**: Agent/command explicitly activates the skill
**Purpose**: Core knowledge and guidance
**Token Cost**: ~500-1500 tokens
**Contains**:
- Core concepts and principles
- Decision-making frameworks
- Standards and best practices
- Common patterns
- Quick reference tables

**Example**:
```markdown
## Instructions

### Packaging Structure

Modern Python projects use `pyproject.toml`:
- Project metadata (name, version, description)
- Dependencies (tool.poetry.dependencies)
- Build system configuration
- Tool-specific settings (pytest, mypy, ruff)

### Best Practices
1. Use `pyproject.toml` over `setup.py`
2. Pin dependency versions for reproducibility
3. Separate dev and production dependencies
...
```

#### Tier 3: Resources (Loaded On Demand)
**When**: Agent/command explicitly requests additional resources
**Purpose**: Detailed examples, reference materials, edge cases
**Token Cost**: ~1000-3000 tokens
**Contains**:
- Complete examples
- Code templates
- Detailed reference tables
- Edge case handling
- Troubleshooting guides

**Example**:
```markdown
## Resources

### Complete pyproject.toml Example
\```toml
[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"

[tool.poetry]
name = "my-package"
version = "0.1.0"
...
\```

### Dependency Management Patterns
...detailed examples...
```

### Activation Strategy

**In Commands**:
```markdown
# Command starts
## Analysis Process

1. Determine project type
2. **Activate skill**: `plugin-architecture-principles` (Tier 2)
3. If detailed examples needed, load Tier 3 resources
4. Apply knowledge to analysis
```

**In Agents**:
```markdown
# Agent definition
You are a Python packaging expert.

**Skills available**:
- `python-packaging-standards` - Activate when analyzing Python projects
- `dependency-management` - Activate when reviewing dependencies

When encountering a Python project:
1. Activate `python-packaging-standards` (Tier 2)
2. Review structure against standards
3. Request Tier 3 resources if edge cases encountered
```

### Token Optimization

**Without Progressive Disclosure** (Always load everything):
- Every invocation: ~3000 tokens of skill knowledge
- 10 invocations: 30,000 tokens
- Much knowledge never used

**With Progressive Disclosure**:
- Metadata (always): ~75 tokens
- Instructions (when needed): +800 tokens
- Resources (rarely): +2000 tokens
- Average: ~875 tokens per invocation
- 10 invocations: ~8,750 tokens (71% savings)

### Design Guidelines

**DO**:
- ✅ Place essential guidance in Instructions
- ✅ Move detailed examples to Resources
- ✅ Keep Metadata concise (title, description, tags)
- ✅ Make each tier independently valuable
- ✅ Reference Resources from Instructions

**DON'T**:
- ❌ Put all knowledge in one section
- ❌ Duplicate information across tiers
- ❌ Load Resources by default
- ❌ Hide essential info in Resources
- ❌ Make tiers interdependent

### Skill Size Targets

| Tier | Target Size | Token Budget | Load Frequency |
|------|------------|--------------|----------------|
| Metadata | 50-100 lines | 75-150 tokens | Always |
| Instructions | 100-300 lines | 500-1500 tokens | When activated |
| Resources | 200-500 lines | 1000-3000 tokens | On explicit request |

### When to Split Skills

If a single skill exceeds these thresholds, consider splitting:

**Too Large** (Instructions > 300 lines):
```
python-standards/  →  python-packaging-standards/
                      python-testing-standards/
                      python-code-quality/
```

**Too Granular** (Instructions < 50 lines):
```
ruff-setup/       →  python-code-quality/
black-setup/          (combine related tools)
mypy-setup/
```

---

## Resources

### Complete Skill Template

```markdown
---
title: [Skill Name]
description: [One sentence description]
tags: [category, topic, use-case]
---

# [Skill Name]

## Metadata

**Purpose**: [What this skill provides]
**Applies to**: [When to use this skill]
**Version**: [Skill version]

---

## Instructions

### [Core Concept 1]
[Essential knowledge that's always needed when skill is activated]

### [Core Concept 2]
[More essential knowledge]

### [Quick Reference]
[Tables, lists, decision frameworks]

**Note**: For detailed examples, see Resources section below.

---

## Resources

### [Detailed Example 1]
[Complete code examples, templates]

### [Edge Case Handling]
[Unusual situations, troubleshooting]

### [Reference Materials]
[Comprehensive tables, detailed guides]
```

### Real-World Example: Documentation Standards

**Metadata** (~75 tokens, always loaded):
```markdown
---
title: Personal Documentation Standards
description: Required documentation for personal use project maturity tiers
tags: [documentation, standards, maturity-tiers]
---
```

**Instructions** (~1000 tokens, loaded when validating docs):
- Tier definitions (Prototype/MVP/Production)
- Required doc types (README, ADRs, diagrams)
- Scoring methodology
- Validation checklist

**Resources** (~2500 tokens, loaded only if needed):
- Complete scoring examples
- Full README template
- Detailed ADR format
- Comprehensive diagram examples

**Usage**:
- Most validations: Metadata + Instructions (~1075 tokens)
- Creating templates: All tiers (~3575 tokens)
- Simple checks: Metadata only (~75 tokens)
