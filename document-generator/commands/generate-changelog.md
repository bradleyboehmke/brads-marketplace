---
description: Create a new CHANGELOG.md file from scratch for a project
---

# Generate Changelog

## Objective

Create a new CHANGELOG.md file following standards (Keep a Changelog format) with entries inferred from git history, supporting both semantic and calendar versioning.

## Activated Skills

1. **`changelog-standards`** (document-generator) - changelog format and structure
2. **`version-validation`** (document-generator) - Versioning rules and validation
3. **`git-history-analysis`** (document-generator) - Git commit parsing patterns

## Parameters

- `--version-type` (optional): `semantic` (default) or `calendar`
- `--format` (optional): `single-file` (default, CHANGELOG.md) or `yearly` (docs/changelog/YYYY.md)
- `--style` (optional): `standard` (default, Keep a Changelog) or `detailed` (Highlights + Technical Details)
- `--path` (optional): Custom changelog location (e.g., `docs/CHANGELOG.md`, `CHANGELOG.md`)
- `--initial-version` (optional): Starting version (default: 0.1.0 for semantic, YYYY.1 for calendar)
- `--tier` (optional): Prototype, MVP, Production

## Process

### 1. Pre-flight Checks

Determine changelog location:
- If `--path` specified: Use that location
- If `--format=yearly`: Use `docs/changelog/YYYY.md`
- Otherwise: Use `CHANGELOG.md` (default)

Check if changelog already exists at target location.

If exists:
```
⚠️  CHANGELOG.md already exists

What would you like to do?
1. Skip - keep existing changelog
2. Backup and regenerate
3. Use /document-generator:update-changelog instead
```

### 2. Detect Version Type

Auto-detect from git tags, `pyproject.toml`, or `package.json`:
- Versions matching `YYYY.N` pattern → CalVer
- Versions matching `X.Y.Z` pattern → SemVer
- `--version-type` parameter → Override
- Default → SemVer

### 3. Analyze Git History

Retrieve all commits from initial commit to HEAD:
```bash
git log --no-merges --pretty=format:"%h|%s|%ad" --date=short
```

Parse commit messages (conventional commits or keyword-based), filter noise, categorize into sections, group related commits, and rephrase in user-facing language.

**Extract PR/issue numbers**: Look for `(#123)`, `#123`, or PR references in commit messages to link entries to GitHub.

### 4. Determine Initial Version

**If `--initial-version` specified**: Use that

**Otherwise**:
- SemVer: Start with `0.1.0` (pre-release) or `1.0.0` (if mature)
- CalVer: Use current year and `.1` (e.g., `2025.1`)

**Ask user if unclear**:
```
What initial version should I use?
1. 0.1.0 (pre-release/prototype)
2. 1.0.0 (stable first release)
3. Custom version
```

### 5. Generate CHANGELOG.md

Choose format based on `--style` parameter:

**Standard style** (default):
```markdown
## [VERSION] - YYYY-MM-DD [TIER]

### Added
- Feature description (#PR)

### Changed
- Change description (#PR)

### Fixed
- Bug fix (#PR)
```

**Detailed style**:
```markdown
## [VERSION] - YYYY-MM-DD [TIER]

### Highlights
- Major feature or improvement (executive summary)
- Critical fix or update

### Detailed Notes

#### Added
- Feature description with technical context (#PR)
  - Sub-detail 1
  - Sub-detail 2

#### Changed
- Change description with rationale (#PR)

#### Fixed
- Bug fix with context (#PR)
```

Include PR/issue links where available from commit messages.

### 6. Write File

Write to determined location:
- `--path` specified: Write to custom path
- `--format=yearly`: Create `docs/changelog/` if needed, write to `docs/changelog/YYYY.md`
- Default: Write to `CHANGELOG.md` in project root

Create parent directories if they don't exist.

### 7. Provide Guidance

```
✓ Created CHANGELOG.md with initial version VERSION

File location: [path]
Version type: [SemVer/CalVer]
Tier: [tier if specified]

Next steps:
1. Review generated entries for accuracy
2. Add any missing user-facing changes
3. Commit the changelog: git add CHANGELOG.md
4. Tag the release: git tag vVERSION
5. Use /document-generator:update-changelog for future updates
```

## Output Format

**Console** (default): Display summary and next steps

**Markdown** (if `--output` specified): Save changelog as markdown file

## Constraints

- Token budget: Keep command concise, delegate to skills
- One changelog per project (single source of truth)
- Focus on user-facing changes only
- No speculation - use actual git history
- Validate version format using `version-validation` skill

## Examples

**Basic usage**:
```bash
/document-generator:generate-changelog
→ Creates CHANGELOG.md with SemVer, starting at 0.1.0
```

**Calendar versioning**:
```bash
/document-generator:generate-changelog --version-type=calendar
→ Creates CHANGELOG.md with CalVer (2025.1)
```

**With tier annotation**:
```bash
/document-generator:generate-changelog --initial-version=1.0.0 --tier=MVP
→ Creates CHANGELOG.md starting at [1.0.0] [MVP]
```

**Yearly format**:
```bash
/document-generator:generate-changelog --format=yearly
→ Creates docs/changelog/2025.md
```

**Custom location**:
```bash
/document-generator:generate-changelog --path=docs/CHANGELOG.md
→ Creates docs/CHANGELOG.md
```

**Detailed style with highlights**:
```bash
/document-generator:generate-changelog --style=detailed
→ Creates CHANGELOG.md with Highlights + Detailed Notes sections
```
