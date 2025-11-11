---
title: README Standards
description: Standard README structure and validation criteria for   projects
tags: [readme, documentation, standards, validation]
---

# README Standards for Personal

## Metadata

**Purpose**: Define   minimal README structure and validation rules
**Version**: 1.0.0

---

## Instructions

### 8-Section Minimal Structure

All Personal READMEs must follow this **minimal structure**:

1. ✅ **Project Title & One-Liner** (REQUIRED)
2. ℹ️ **Badges Block** (OPTIONAL - include for MVP/Production tiers)
3. ✅ **Short Description** (REQUIRED - must integrate business problem/solution)
4. ✅ **Installation** (REQUIRED)
5. ✅ **Documentation** (REQUIRED - can be dedicated section or part of guides/resources section)
6. ℹ️ **Supporting Components** (OPTIONAL - only if dependencies exist)
7. ✅ **Contributing Link** (REQUIRED - can be dedicated section or link within documentation section)
8. ✅ **Issue Reporting** (REQUIRED - can be dedicated bugs section or link within documentation/contributing)

**Key principles**:
- **Link-first**: Point to detailed docs, don't embed everything inline
- **Concise**: Keep README minimal, use links for depth
- **Flexible structure**: Section names can vary (e.g., "Description" or "Overview", "Guides" can contain contributing/docs links)
- **Essential content over format**: Ensure contributing links and issue reporting exist, regardless of exact section structure
- **Actionable**: Clear installation steps and contribution guidance

---

### Section Validation Matrix

| Section | Heading | Required Content | Validation Checks |
|---------|---------|------------------|-------------------|
| **1. Title & One-Liner** | `# {Name}` | 1-2 sentence description | ✅ Title present<br>✅ Specific description (not vague) |
| **2. Badges** *(optional)* | `<!-- badges: start -->`<br>`...badges...`<br>`<!-- badges: end -->` | Version, Lifecycle, Docs (MVP/Production)<br>+ Python version, Code Style, Pre-commit (Production Python projects) | ℹ️ Note if missing (MVP/Production tier)<br>✅ Wrapped in HTML comments<br>✅ shields.io format<br>✅ Lifecycle color matches tier (orange/yellow/green)<br>⚠️ Python badges on non-Python projects |
| **3. Description** | `## Description` or `## Overview` | Business problem + solution + functionality (3-5 sentences) | ✅ Heading present (Description/Overview acceptable)<br>✅ Business context included<br>ℹ️ Separate Business Problem section allowed if brief |
| **4. Installation** | `## Installation` | Actionable command + optional setup link | ✅ Code block with command<br>✅ Link to `docs/setup.md` if exists |
| **5. Documentation** | `## Documentation` or within `## Guides` | Bulleted links (only existing docs) | ✅ 1+ link provided<br>✅ ADRs linked if `adr/` exists<br>✅ Links valid (no placeholders) |
| **6. Supporting Components** *(optional)* | `## Supporting Components` | Dependency list with links | ℹ️ Skip for standalone projects<br>✅ Each dependency has link + description |
| **7. Contributing Link** | `## Contributing` or within `## Documentation`/`## Guides` | Link to CONTRIBUTING.md or inline guidance | ✅ Contributing link/guidance present (dedicated section OR within docs section)<br>✅ Link if CONTRIBUTING.md exists<br>⚠️ Suggest CONTRIBUTING.md for MVP/Production |
| **8. Issue Reporting** | `## Bugs`, `## Bugs & Enhancements`, or within `## Contributing` | Issue tracker link | ✅ Issue reporting link present (dedicated section OR within contributing/docs)<br>✅ Clear call-to-action |

**Common validation flags**:
- ✅ **Compliant** - Section meets all requirements
- ⚠️ **Incomplete** - Section present but missing key content
- ❌ **Non-compliant** - Wrong structure (e.g., separate Business Problem section)
- ℹ️ **Optional** - Note if missing but don't fail validation

---

### Tier-Specific Requirements

| **Section** | **Prototype** | **MVP** | **Production** |
|-------------|---------------|---------|----------------|
| **Title & One-Liner** | Required | Required | Required |
| **Badges** | Optional (usually skip or lifecycle only) | Version, Lifecycle (yellow), Docs | Full set: Version, Lifecycle (green), Docs, Python version (if applicable), Code style, Pre-commit |
| **Description** | Required (2-3 sentences) | Required (3-4 sentences) | Required (4-5 sentences) |
| **Installation** | Required | Required | Required |
| **Documentation** | Required (minimal) | Required (moderate) | Required (comprehensive) |
| **Supporting Components** | Usually none | May have 1-2 | Often multiple |
| **Contributing** | Required (inline OK) | Required (CONTRIBUTING.md preferred) | Required (CONTRIBUTING.md required) |
| **Bugs** | Required | Required | Required |

**Tier detection signals**:
- **Prototype**: No CI/CD, minimal tests, research-focused, `docs/` sparse
- **MVP**: Basic CI/CD, test coverage setup, some docs, pilot deployment
- **Production**: Full CI/CD, comprehensive tests, extensive docs, production deployment

---

### Link Validation Rules

**Required link checks**:
1. **Architecture docs**: If `docs/architecture.md` or `.drawio` exists, must be linked in Documentation section
2. **ADRs**: If `adr/` directory exists with ADRs, must be linked in Documentation section
3. **CONTRIBUTING.md**: If exists, must be linked in Contributing section
4. **Setup guide**: If `docs/setup.md` exists, should be linked in Installation section

**Broken link detection**:
- Verify relative links point to existing files
- Flag broken links as compliance issue
- Don't flag external URLs (assume valid unless HTTP check requested)

---

### Common Compliance Issues

**Issue 1: Separate Business Problem/Solution sections**
- ℹ️ Acceptable: `## Business Problem` and `## Solution` as separate sections (if brief and focused)
- ✅ Preferred: Integrate into `## Description` or `## Overview` paragraph for conciseness

**Issue 2: Embedding full setup instructions**
- ❌ Non-compliant: Detailed setup steps in README Installation section
- ✅ Fix: Simple install command + link to `docs/setup.md`

**Issue 3: Missing business context**
- ⚠️ Incomplete: Description only has technical details, no problem/solution context
- ✅ Fix: Add sentence explaining what business problem this solves

**Issue 4: Placeholder documentation links**
- ❌ Non-compliant: Linking to `docs/architecture.md` when file doesn't exist
- ✅ Fix: Only link to docs that exist; note missing docs in validation report

**Issue 5: Testing instructions in README**
- ❌ Non-compliant: Full testing guide embedded in README
- ✅ Fix: Move testing instructions to `CONTRIBUTING.md`, link from README

**Issue 6: Missing badges for Production project**
- ⚠️ Incomplete: Production-tier project without badges
- ✅ Fix: Add full badge set (version, lifecycle-green, docs, Python version, code style, pre-commit)

**Issue 7: Badges not wrapped in HTML comments**
- ⚠️ Incomplete: Badges present but missing `<!-- badges: start/end -->` wrappers
- ✅ Fix: Wrap badge block in HTML comments for maintainability

**Issue 8: Incorrect lifecycle badge color**
- ⚠️ Incomplete: MVP project with "experimental" (orange) badge instead of "mvp" (yellow)
- ✅ Fix: Match lifecycle badge color to project tier (orange=prototype, yellow=mvp, green=production)

**Issue 9: Python badges on non-Python project**
- ❌ Non-compliant: Python version, black, or ruff badges on JavaScript/other project
- ✅ Fix: Remove language-specific badges from non-applicable projects

---

### Integration with MTPS (Minimum Transferrable Project Standards)

The README standards align with   MTPS requirements:

**Documentation Standard** (from MTPS):
- README.md with business problem, solution, setup → ✅ Covered by sections 1, 3, 4
- Architecture diagram or description → ✅ Linked in Documentation section
- Handoff summary → ✅ Separate document (not in README)

**README's role in MTPS**:
- Entry point to project documentation
- Links to architecture, ADRs, contributing guides
- Does NOT replace comprehensive documentation
- Minimal structure keeps it maintainable

---

## Resources

### Validation Checklist

Use this checklist when validating READMEs:

**Structure (8 sections)**:
- [ ] Project Title & One-Liner present
- [ ] Badges block (note if missing for MVP/Production, validate format if present)
- [ ] Short Description present (## Description or ## Overview acceptable)
- [ ] Installation section present
- [ ] Documentation links present (dedicated section OR within ## Guides/etc.)
- [ ] Supporting Components (note if missing, don't fail)
- [ ] Contributing link present (dedicated section OR within ## Documentation/## Guides)
- [ ] Issue reporting link present (dedicated ## Bugs section OR within ## Contributing/docs)

**Content Quality**:
- [ ] One-liner is specific and descriptive
- [ ] Badges wrapped in `<!-- badges: start/end -->` comments (if present)
- [ ] Lifecycle badge color matches tier: orange (prototype), yellow (mvp), green (production)
- [ ] No Python-specific badges on non-Python projects
- [ ] Description includes business problem/solution context (integrated or separate sections acceptable)
- [ ] Installation command is actionable
- [ ] Documentation links are valid (point to existing files)
- [ ] ADRs linked if `adr/` exists
- [ ] CONTRIBUTING.md linked if exists (can be in dedicated section or docs/guides section)
- [ ] Issue tracker link or reporting guidance provided (can be in dedicated section or contributing/docs section)

**Formatting**:
- [ ] Proper heading hierarchy (`#` for title, `##` for sections)
- [ ] Code blocks have language identifiers
- [ ] Links use descriptive text
- [ ] Consistent list formatting

**Tier-appropriate**:
- [ ] Badges present for MVP/Production (optional for Prototype)
- [ ] Badge set matches tier (MVP: basic set, Production: full set)
- [ ] Documentation depth matches tier
- [ ] CONTRIBUTING.md exists for MVP/Production

**Badge-specific validation** (if badges present):
- [ ] Wrapped in HTML comments (`<!-- badges: start -->` ... `<!-- badges: end -->`)
- [ ] Version/Release badge present (if project has releases)
- [ ] Lifecycle badge present with correct color for tier
- [ ] Docs badge present for MVP/Production (if docs exist)
- [ ] Python version badge only on Python projects
- [ ] Code style badges (black, ruff) only on Python projects with those tools
- [ ] Pre-commit badge only if `.pre-commit-config.yaml` exists

---

### Compliance Report Format

When generating validation reports, use this format:

```markdown
# README Validation Report

**Project**: {Project Name}
**Date**: {Date}
**Tier**: {Detected Tier}

## Summary

- ✅ {X} sections compliant
- ⚠️ {Y} sections incomplete
- ❌ {Z} sections missing

## Detailed Assessment

### ✅ Compliant Sections

1. **Title & One-Liner** - Clear and descriptive
2. **Installation** - Simple command with link to setup guide
3. **Bugs & Enhancements** - Issue tracker linked

### ⚠️ Incomplete Sections

4. **Short Description** - Missing business problem context
   - **Recommendation**: Add sentence explaining what business problem this solves

5. **Documentation** - Minimal links provided
   - **Recommendation**: Add links to architecture docs and ADRs (`adr/` exists but not linked)

### ❌ Missing Sections

6. **Contributing** - Section not found
   - **Recommendation**: Create Contributing section or add `CONTRIBUTING.md`

## Recommendations

1. **Priority 1 (Required)**:
   - Add Contributing section
   - Integrate business problem into Description

2. **Priority 2 (Suggested)**:
   - Link to existing ADRs in Documentation section
   - Create architecture documentation

3. **Priority 3 (Optional)**:
   - Add badges (project is MVP tier)
   - Create quickstart guide

## Next Steps

Run `/document-generator:update-readme` to automatically fix missing sections.
```

---

### Before/After Examples

**Before (non-compliant)**:
```markdown
# My Project

This is a Python project.

## Setup

Install dependencies and run the code.

## Usage

See the code.
```

**After (compliant - Prototype tier)**:
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

- See notebooks in `notebooks/` for exploratory analysis and model training
- Model card available in `docs/model-card.md`

## Contributing

This is an experimental prototype. For questions or suggestions, contact the data science team.

## Bugs & Enhancements

Report issues via [GitHub Issues](https://github.com/USERNAME/churn-predictor/issues).
```

---

**Before (outdated structure)**:
```markdown
# Feature Store

## Business Problem
Data scientists extract features redundantly.

## Solution
Centralized feature store.

## Architecture
[Architecture diagram here]

## Setup
1. Install Python 3.9
2. Install dependencies
3. Configure database
4. Run migrations
5. Start server
...

## Testing
Run pytest with coverage.
...
```

**After (compliant - MVP tier)**:
```markdown
# Feature Store API

![Version](https://img.shields.io/badge/version-0.2.0-blue)
![Lifecycle](https://img.shields.io/badge/lifecycle-mvp-yellow)

RESTful API for serving customer features to ML models and analytics tools.

## Description

Data scientists and ML engineers need consistent, versioned access to customer features across multiple projects, but currently extract features redundantly from raw data sources. This API provides a centralized feature store with versioning, caching, and real-time serving capabilities.

## Installation

\`\`\`bash
pip install feature-store-client
\`\`\`

For local development setup, see [Setup Guide](docs/setup.md).

## Documentation

- [Quickstart Guide](docs/quickstart.md) - Get started in 5 minutes
- [API Reference](docs/api.md) - Complete endpoint documentation
- [Architecture](docs/architecture.md) - System design and data flow
- [ADRs](adr/) - Architecture Decision Records

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on reporting bugs, submitting changes, and running tests.

## Bugs & Enhancements

Report bugs and request features via [GitHub Issues](https://github.com/USERNAME/feature-store-api/issues).
```

---

### Tier-Specific Requirements Matrix

| **Validation Check** | **Prototype** | **MVP** | **Production** |
|----------------------|---------------|---------|----------------|
| **Title & One-Liner** | Required | Required | Required |
| **Badges** | Optional | Recommended | Required |
| **Description Length** | 2-3 sentences min | 3-4 sentences min | 4-5 sentences min |
| **Business Context** | Preferred | Required | Required |
| **Installation Command** | Required | Required | Required |
| **Setup Guide Link** | Optional | Recommended | Required |
| **Documentation Links** | 1+ link | 3+ links | 5+ links |
| **Architecture Docs** | Optional | Recommended | Required |
| **ADRs** | Optional | Recommended | Required (if exist) |
| **CONTRIBUTING.md** | Optional | Recommended | Required |
| **Supporting Components** | Usually none | If applicable | If applicable |
| **Issue Tracker Link** | Required | Required | Required |

---

### Progressive Validation Approach

**Level 1: Structure** (must pass):
- All 6 required sections present (Title, Description, Installation, Documentation, Contributing, Bugs)
- Proper heading hierarchy

**Level 2: Content** (should pass):
- Business problem/solution in Description
- Actionable installation command
- Valid documentation links
- Clear contributing guidance

**Level 3: Quality** (nice to have):
- Tier-appropriate badges
- Comprehensive documentation links
- CONTRIBUTING.md for mature projects
- Architecture docs linked

**Scoring**:
- **Level 1 pass** = Minimal compliance ✅
- **Level 2 pass** = Standard compliance ✅✅
- **Level 3 pass** = Excellent compliance ✅✅✅

---

**Remember**: The goal is **minimal, consistent READMEs** that serve as entry points. Link to comprehensive documentation rather than embedding everything inline.
