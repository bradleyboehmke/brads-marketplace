---
title: Changelog Standards
description: Standard changelog format based on Keep a Changelog
tags: [changelog, versioning, documentation, standards]
---

# Changelog Standards

## Metadata

**Purpose**: Define Standard changelog format and structure
**Version**: 1.0.0

---

## Format Specification

Based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/) with Personal extensions.

## File Locations

**Flexible locations** - Teams can choose where to store changelogs:
- `CHANGELOG.md` (project root) - Most common
- `docs/CHANGELOG.md` - Documentation directory
- `docs/changelog/YYYY.md` - Yearly split format for long-lived projects
- Custom paths supported via `--path` parameter

**Auto-detection order**:
1. `CHANGELOG.md` (root)
2. `docs/CHANGELOG.md`
3. `docs/changelog/YYYY.md` (current year)
4. Search for `**/CHANGELOG.md` or `**/changelog/*.md`

## Version Heading Format

### Semantic Versioning (SemVer)
```markdown
## [2.9.0] - 2024-03-15 [MVP]
```

### Calendar Versioning (CalVer)
```markdown
## [2025.1] - 2025-01-15 [Prototype]
```

**Components**:
- Version in brackets: `[X.Y.Z]` or `[YYYY.N]`
- ISO date: `YYYY-MM-DD`
- Tier annotation (optional): `[Prototype]`, `[MVP]`, or `[Production]`

## Changelog Styles

### Standard Style (Default)

Uses Keep a Changelog sections in this order:

1. **Added** - New features
2. **Changed** - Changes to existing functionality
3. **Deprecated** - Soon-to-be-removed features
4. **Removed** - Removed features
5. **Fixed** - Bug fixes
6. **Security** - Security fixes

**Example**:
```markdown
### Added
- New data validation pipeline for customer segments (#142)
- Support for weekly aggregation in metrics (#156)

### Fixed
- Corrected timezone handling in datetime conversion (#158)
```

### Detailed Style

Uses Highlights + Technical Details format for comprehensive release notes:

**Structure**:
```markdown
## [VERSION] - YYYY-MM-DD [TIER]

### Highlights

Brief executive summary (2-4 key points):
- Major feature or capability added
- Significant improvements or changes
- Critical fixes or updates

### Detailed Notes

#### Added
- Feature description with technical details (#PR-number)

#### Changed
- Change description with rationale (#PR-number)

#### Fixed
- Bug fix with context (#PR-number)
```

**Example**:
```markdown
## [2.1.0] - 2025-11-15 [MVP]

### Highlights

- Introduced automated changelog generation from git history
- Enhanced documentation workflow with standards validation
- Improved token efficiency through command optimization

### Detailed Notes

#### Added
- Changelog standardization capability with SemVer and CalVer support (#12)
  - Generate new CHANGELOG.md from git history
  - Update existing changelogs with recent commits
  - Validate format against standards
- Custom path support for flexible changelog locations (#12)

#### Changed
- Optimized git-workflow commands for token efficiency (#23)
- Refactored validation logic to reduce redundancy (#23)

#### Fixed
- Corrected file size validation in pre-commit checks (#23)
```

## Unreleased Section

Always include at top of changelog:
```markdown
## [Unreleased]

### Added
- Feature in development

### Changed
- Work in progress
```

## Complete Example

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [Unreleased]

### Added
- Experimental feature X

## [2.1.0] - 2025-11-01 [MVP]

### Added
- Customer segmentation model v2
- Automated retraining pipeline

### Changed
- Updated evaluation metrics to include precision-recall curves

### Fixed
- Memory leak in batch processing

## [2.0.0] - 2025-09-15 [MVP]

### Added
- Initial MVP release
- Core recommendation engine
- Integration with production data warehouse

### Changed
- Migrated from prototype to production-ready architecture

[2.1.0]: https://github.com/org/repo/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/org/repo/releases/tag/v2.0.0
```

## Version Comparison Links

At bottom of changelog, include links:
```markdown
[2.1.0]: https://github.com/org/repo/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/org/repo/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/org/repo/releases/tag/v1.0.0
```

## Tier Annotations

Map project maturity to versions:

- **[Prototype]** - Experimental, research phase
- **[MVP]** - Pilot, initial production deployment
- **[Production]** - Stable, fully supported release

## Writing Guidelines

**Good entries**:
- Clear, concise descriptions
- User-facing changes (what, not how)
- Business impact when relevant
- Link to issues/PRs for details

**Bad entries**:
- Implementation details
- Commit messages verbatim
- Internal refactoring (unless user-visible)

**Example Good Entry**:
```markdown
### Added
- Support for multi-year trend analysis in dashboard (#142)
```

**Example Bad Entry**:
```markdown
### Changed
- Refactored utils.py to use dataclasses instead of dicts
```
