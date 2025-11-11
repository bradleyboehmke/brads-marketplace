---
title: Version Validation
description: Validation rules for semantic and calendar versioning
tags: [versioning, semver, calver, validation]
---

# Version Validation

## Metadata

**Purpose**: Validation rules for semantic and calendar versioning
**Version**: 1.0.0

---

## Version Types

### Semantic Versioning (SemVer)

**Format**: `MAJOR.MINOR.PATCH` (e.g., 2.9.1)

**Rules**:
- MAJOR: Breaking changes, incompatible API changes
- MINOR: New features, backward-compatible
- PATCH: Bug fixes, backward-compatible

**Examples**:
- `1.0.0` - Initial stable release
- `1.1.0` - Added new feature
- `1.1.1` - Fixed bug
- `2.0.0` - Breaking change

**Regex Pattern**: `^\d+\.\d+\.\d+$`

### Calendar Versioning (CalVer)

**Format**: `YYYY.MINOR` or `YYYY.MM.PATCH` (e.g., 2025.1 or 2025.11.2)

**Rules**:
- YYYY: Year (4 digits)
- MINOR: Sequential release number within year (starts at 1)
- MM: Month (01-12)
- PATCH: Bug fix number within month

**Examples**:
- `2025.1` - First release of 2025
- `2025.2` - Second release of 2025
- `2025.11.1` - First patch in November 2025

**Regex Patterns**:
- Year.Minor: `^\d{4}\.\d+$`
- Year.Month.Patch: `^\d{4}\.(0[1-9]|1[0-2])\.\d+$`

## Version Detection

**Auto-detect version type** from existing versions:

1. Check existing changelog for version patterns
2. Check git tags: `git tag --list`
3. Check project metadata:
   - Python: `pyproject.toml` or `setup.py`
   - Node: `package.json`
4. Default to SemVer if ambiguous

**Detection Logic**:
```
If version matches YYYY.N pattern → CalVer
If version matches X.Y.Z pattern → SemVer
If no existing versions → Ask user or default to SemVer
```

## Validation Rules

### Chronological Ordering

Versions MUST appear in reverse chronological order (newest first):

**Correct**:
```markdown
## [2.1.0] - 2025-11-01
## [2.0.0] - 2025-09-15
## [1.5.0] - 2025-06-10
```

**Incorrect**:
```markdown
## [1.5.0] - 2025-06-10
## [2.0.0] - 2025-09-15  ❌ Out of order
## [2.1.0] - 2025-11-01
```

### Version Increment Rules

**SemVer**:
- MAJOR increments reset MINOR and PATCH to 0 (2.3.1 → 3.0.0)
- MINOR increments reset PATCH to 0 (2.3.1 → 2.4.0)
- PATCH increments by 1 (2.3.1 → 2.3.2)

**CalVer (Year.Minor)**:
- Year changes reset MINOR to 1 (2024.5 → 2025.1)
- Within same year, MINOR increments (2025.1 → 2025.2)

**CalVer (Year.Month.Patch)**:
- New month resets PATCH to 1 (2025.10.3 → 2025.11.1)
- Within same month, PATCH increments (2025.11.1 → 2025.11.2)

### Date Validation

Dates MUST:
- Use ISO format: `YYYY-MM-DD`
- Be valid dates (no Feb 30, etc.)
- Match or precede version dates in chronological order
- Not be in the future (warning, not error)

**Regex**: `^\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12]\d|3[01])$`

## Common Validation Errors

| Error Type | Example | Issue | Fix |
|------------|---------|-------|-----|
| **Invalid Version Format** | `## [v2.1.0] - 2025-11-01`<br>`## [2.1] - 2025-11-01`<br>`## [25.1] - 2025-11-01` | 'v' prefix in brackets<br>Incomplete SemVer (missing PATCH)<br>Incomplete year (use 2025, not 25) | Remove prefix, use complete version format |
| **Incorrect Date Format** | `## [2.1.0] - 11/01/2025`<br>`## [2.1.0] - 2025-Nov-01`<br>`## [2.1.0] - 2025-11-1` | Wrong format (MM/DD/YYYY)<br>Month as text<br>Missing leading zero | Use `YYYY-MM-DD` format |
| **Version Skip** | `## [2.1.0] - 2025-11-01`<br>`## [1.9.0] - 2025-09-15` | Skipped version 2.0.0 | Warning - may indicate missing entry |
| **Date Ordering** | `## [2.1.0] - 2025-09-01`<br>`## [2.0.0] - 2025-11-01` | Later date for earlier version | Ensure dates are chronological |

## Version Comparison

**SemVer Comparison**:
```
2.1.0 > 2.0.5 > 2.0.0 > 1.9.9
```

**CalVer Comparison** (Year.Minor):
```
2025.5 > 2025.1 > 2024.12 > 2024.1
```

**CalVer Comparison** (Year.Month.Patch):
```
2025.11.2 > 2025.11.1 > 2025.10.5 > 2024.12.1
```

## Auto-increment Logic

**SemVer**:
- For features: Increment MINOR (2.1.3 → 2.2.0)
- For fixes: Increment PATCH (2.1.3 → 2.1.4)
- For breaking changes: Increment MAJOR (2.1.3 → 3.0.0)

**CalVer (Year.Minor)**:
- Same year: Increment MINOR (2025.1 → 2025.2)
- New year: Reset to YEAR.1 (2024.5 → 2025.1)

**CalVer (Year.Month.Patch)**:
- Same month: Increment PATCH (2025.11.1 → 2025.11.2)
- New month: YEAR.MONTH.1 (2025.10.3 → 2025.11.1)

## Validation Functions

**Validate version format**:
- Match against regex for SemVer or CalVer
- Return error if no match

**Validate version sequence**:
- Parse all versions in changelog
- Sort by version number
- Check for correct ordering
- Check for skipped versions

**Validate dates**:
- Parse all dates
- Check ISO format
- Check chronological consistency
- Warn if future dates

**Suggest next version**:
- Detect version type
- Analyze git history since last version
- Apply increment rules
- Return suggested version
