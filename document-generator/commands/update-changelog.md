---
description: Update existing CHANGELOG.md with new entries from recent commits
---

# Update Changelog

## Objective

Update existing CHANGELOG.md with new version entries based on recent git commits, maintaining standards and proper version sequencing.

## Activated Skills

1. **`changelog-standards`** (document-generator) - changelog format and structure
2. **`version-validation`** (document-generator) - Versioning rules and validation
3. **`git-history-analysis`** (document-generator) - Git commit parsing patterns

## Parameters

- `--path` (optional): Changelog location (auto-detects if not specified)
- `--style` (optional): Inherit from existing changelog or specify `standard`/`detailed`
- `--since` (optional): Git ref to start from (default: last version tag or last changelog entry)
- `--new-version` (optional): Version for new release (auto-increment if not provided)
- `--tier` (optional): Update tier annotation (Prototype, MVP, Production)
- `--draft` (optional): Add to [Unreleased] section instead of creating versioned release

## Process

### 1. Locate and Read Changelog

Locate changelog file:
- If `--path` specified: Use that location
- Otherwise auto-detect from standard locations:
  - `CHANGELOG.md` (root)
  - `docs/CHANGELOG.md`
  - `docs/changelog/YYYY.md` (current year)
  - Search for `**/CHANGELOG.md` or `**/changelog/*.md`

If not found:
```
❌ No CHANGELOG.md found

Run /document-generator:generate-changelog to create one first.
```

Read and parse existing changelog:
- Extract current version
- Detect version type (SemVer vs CalVer)
- Identify format (single-file vs yearly)
- Detect style (standard vs detailed) from existing structure

### 2. Determine Commit Range

**Find last version**:
```bash
# From changelog
grep -E "^## \[" CHANGELOG.md | head -n 2 | tail -n 1

# From git tags
git describe --tags --abbrev=0 2>/dev/null
```

**Get commits since last version**:
```bash
# If last tag exists
git log LAST_TAG..HEAD --no-merges --pretty=format:"%h|%s|%ad" --date=short

# If no tags (first release since changelog creation)
git log --since="$(git log -1 --format=%ai CHANGELOG.md)" --no-merges --pretty=format:"%h|%s|%ad" --date=short
```

If no new commits:
```
ℹ️  No new commits since last version

Changelog is up-to-date.
```

### 3. Analyze New Commits

Parse commit messages, categorize into sections, filter noise, group related changes, and transform to user-facing language.

**Extract PR/issue numbers** from commit messages to include as links.

### 4. Determine New Version

**If `--new-version` specified**: Use that (validate with `version-validation` skill)

**If `--draft` flag**: Add to [Unreleased] section

**Otherwise, auto-increment**:

**For SemVer**:
- If "feat" or "Added" entries → Increment MINOR (2.1.0 → 2.2.0)
- If only "fix" or "Fixed" entries → Increment PATCH (2.1.0 → 2.1.1)
- If breaking changes detected → Suggest MAJOR (2.1.0 → 3.0.0)

**For CalVer (Year.Minor)**:
- Same year → Increment MINOR (2025.1 → 2025.2)
- New year → Reset to YEAR.1 (2024.5 → 2025.1)

**Ask user for confirmation**:
```
Based on commits, I suggest version: [suggested-version]

Changes detected:
- X new features (Added)
- Y bug fixes (Fixed)
- Z improvements (Changed)

What version should I use?
1. [suggested-version] (recommended)
2. Specify custom version
3. Add to [Unreleased] instead
```

### 5. Insert New Version Section

Format new entry based on detected or specified style:

**Standard style**:
```markdown
## [NEW_VERSION] - YYYY-MM-DD [TIER]

### Added
- Feature description (#PR)

### Changed
- Improvement description (#PR)

### Fixed
- Bug fix (#PR)
```

**Detailed style**:
```markdown
## [NEW_VERSION] - YYYY-MM-DD [TIER]

### Highlights
- Major capability added
- Significant improvement made

### Detailed Notes

#### Added
- Feature with technical context (#PR)

#### Changed
- Change with rationale (#PR)

#### Fixed
- Fix with context (#PR)
```

**Insert location**:
- After "## [Unreleased]" section
- Before previous version entries
- Maintain reverse chronological order

**Update [Unreleased] section**:
- Remove entries that moved to new version
- Keep any remaining draft entries

### 6. Update Version Comparison Links

At bottom of changelog, add/update links:

```markdown
[NEW_VERSION]: https://github.com/ORG/REPO/compare/vOLD_VERSION...vNEW_VERSION
[OLD_VERSION]: https://github.com/ORG/REPO/compare/vPREV_VERSION...vOLD_VERSION
```

Extract repo URL from:
```bash
git config --get remote.origin.url
```

### 7. Write Updated Changelog

Validate with `version-validation` skill:
- Version format correct
- Chronological ordering maintained
- No version skips
- Dates are valid

Write updated file back to original location.

### 8. Provide Guidance

```
✓ Updated CHANGELOG.md with version NEW_VERSION

Changes:
- Added: X entries
- Changed: Y entries
- Fixed: Z entries

Next steps:
1. Review the new changelog entries
2. Commit changes: git add CHANGELOG.md
3. Tag release: git tag vNEW_VERSION
4. Push with tags: git push --tags
```

## Output Format

**Console** (default): Display summary and next steps

**Markdown** (if `--output` specified): Save updated changelog

## Special Cases

### Draft Mode (--draft)

Add to [Unreleased] instead of creating versioned release:

```markdown
## [Unreleased]

### Added
- New feature in development

### Fixed
- Bug fix awaiting release
```

Use this when:
- Changes not ready for release
- Accumulating changes before version bump
- Working in feature branch

### Empty Unreleased Section

If [Unreleased] section exists but is empty, preserve it:

```markdown
## [Unreleased]

## [1.2.0] - 2025-11-11
```

### Multiple Version Formats

If changelog contains both CalVer and SemVer (migration scenario):
- Detect most recent format
- Warn user about mixed formats
- Suggest standardizing

## Examples

**Basic usage**:
```bash
/document-generator:update-changelog
→ Auto-detects last version, suggests next version, updates changelog
```

**With specific version**:
```bash
/document-generator:update-changelog --new-version=2.1.0
→ Creates version 2.1.0 entry with recent commits
```

**Draft mode**:
```bash
/document-generator:update-changelog --draft
→ Adds commits to [Unreleased] section
```

**With tier annotation**:
```bash
/document-generator:update-changelog --new-version=1.0.0 --tier=MVP
→ Creates [1.0.0] [MVP] entry
```

**Since specific ref**:
```bash
/document-generator:update-changelog --since=v1.5.0
→ Includes all commits since v1.5.0 tag
```

**Custom location**:
```bash
/document-generator:update-changelog --path=docs/CHANGELOG.md
→ Updates changelog at docs/CHANGELOG.md
```

## Constraints

- Token budget: Keep concise, delegate to skills
- Preserve existing changelog structure
- Maintain chronological order
- Validate all version increments
- No data loss - backup approach recommended
