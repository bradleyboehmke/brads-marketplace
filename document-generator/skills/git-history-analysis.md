---
title: Git History Analysis
description: Patterns for parsing git commits and PRs to infer changelog entries
tags: [git, commits, changelog, parsing]
---

# Git History Analysis

## Metadata

**Purpose**: Extract changelog entries from git history
**Version**: 1.0.0

---

## Git Log Commands

### Retrieve Commits in Range

**All commits since last tag**:
```bash
git log $(git describe --tags --abbrev=0)..HEAD --pretty=format:"%h|%s|%an|%ad" --date=short
```

**All commits since specific date**:
```bash
git log --since="2025-01-01" --pretty=format:"%h|%s|%an|%ad" --date=short
```

**All commits between two refs**:
```bash
git log v1.0.0..v2.0.0 --pretty=format:"%h|%s|%an|%ad" --date=short
```

**Format explained**:
- `%h` - Short commit hash
- `%s` - Subject/title
- `%an` - Author name
- `%ad` - Author date
- `|` - Delimiter for parsing

### Exclude Noise Commits

**Filter out merge commits**:
```bash
git log --no-merges
```

**Filter out version bump commits**:
```bash
git log --grep="^Bump version" --invert-grep
```

**Combined filters**:
```bash
git log --no-merges --grep="^Bump version\|^Release" --invert-grep
```

## Commit Message Parsing

### Conventional Commits

**Format**: `<type>(<scope>): <description>`

See "Changelog Section Mapping" table below for complete type-to-section mappings.

**Examples**:
```
feat(api): add customer export endpoint → Added
fix(auth): resolve timeout on login → Fixed
perf(db): optimize query performance → Changed
security(deps): update vulnerable packages → Security
```

**Parsing regex**: `^(feat|fix|docs|refactor|perf|test|chore|security)(\([^\)]+\))?: (.+)$`

### Non-Conventional Commits

**Keyword-based categorization**:

**Added indicators**:
- Starts with: "Add", "Implement", "Introduce", "Create"
- Contains: "new feature", "support for"

**Fixed indicators**:
- Starts with: "Fix", "Resolve", "Correct", "Patch"
- Contains: "bug", "issue", "error", "crash"

**Changed indicators**:
- Starts with: "Update", "Improve", "Enhance", "Optimize", "Refactor"
- Contains: "performance", "efficiency"

**Removed indicators**:
- Starts with: "Remove", "Delete", "Drop"
- Contains: "deprecated", "legacy"

**Security indicators**:
- Contains: "security", "vulnerability", "CVE-", "XSS", "injection"

**Example classification**:
```
"Add customer segmentation feature" → Added
"Fix memory leak in batch processing" → Fixed
"Update data validation logic" → Changed
"Remove deprecated API endpoints" → Removed
"Patch security vulnerability in auth" → Security
```

## PR Title Parsing

GitHub/GitLab PR titles often follow similar patterns:

**PR number extraction**:
```bash
gh pr list --state merged --limit 100 --json number,title,mergedAt
```

**Parse PR titles** using same rules as commit messages

**Prefer PR titles over commits** when available (cleaner, more user-facing)

## Extracting PR/Issue References

**From commit messages**:
- Pattern 1: `(#123)` at end of message
- Pattern 2: `#123` anywhere in message
- Pattern 3: `Merge pull request #123`
- Pattern 4: `Fixes #123`, `Closes #123`, `Resolves #123`

**From PR list**:
```bash
# Get PR number associated with commit
gh pr list --state merged --search "sha:COMMIT_HASH" --json number
```

**Link format in changelog**:
- Short form: `(#123)` for PR/issue number
- Full entries: `- Feature description (#123)`
- Multi-ref: `- Feature description (#123, #124)`

## Filtering Strategy

### Skip These Commits

**Merge commits**:
- Pattern: `^Merge (branch|pull request)`

**Version bumps**:
- Pattern: `^(Bump|Release|Version) (version )?[0-9]`

**Internal housekeeping**:
- Pattern: `^(chore|ci|test|docs):`
- Exception: Major docs overhauls might be "Added"

**WIP commits**:
- Pattern: `^WIP:`, `^temp:`, `^tmp:`

### Grouping and Deduplication

**Group by scope** (if using conventional commits):
```
feat(api): add export endpoint
feat(api): add import endpoint
→ Group under "API" subsection in Added
```

**Deduplicate similar commits**:
```
fix: typo in validation message
fix: another typo in error message
→ Combine as "Fixed typos in validation messages"
```

**Squash implementation details**:
```
feat: add customer export (part 1)
feat: add customer export (part 2)
feat: finalize customer export
→ Single entry: "Customer export feature"
```

## Changelog Section Mapping

**Type → Section mapping**:

| Commit Type | Changelog Section | Notes |
|-------------|-------------------|-------|
| `feat` | Added | New features |
| `fix` | Fixed | Bug fixes |
| `perf` | Changed | Performance improvements |
| `refactor` | Changed | Only if user-facing |
| `security` | Security | Security patches |
| `deprecate` | Deprecated | Features marked for removal |
| `remove` | Removed | Deleted features |
| `docs` | (Skip) | Unless major docs addition |
| `test` | (Skip) | Internal only |
| `chore` | (Skip) | Internal only |
| `ci` | (Skip) | Internal only |

## Extracting User-Facing Changes

**Focus on impact, not implementation**:

**Good**: "Added support for multi-year trend analysis"
**Bad**: "Refactored TrendAnalyzer class to support configurable date ranges"

**Transformation examples**:

```
Git: "refactor: extract validation logic to separate module"
→ Skip (internal refactoring)

Git: "feat: implement caching layer for API responses"
→ Added: "API response caching for improved performance"

Git: "fix: handle edge case in date parsing"
→ Fixed: "Corrected date parsing for edge cases"

Git: "perf(db): add indexes to customer table"
→ Changed: "Improved database query performance"
```

## Git Commands Summary

**Get commits since last version**:
```bash
git log $(git describe --tags --abbrev=0)..HEAD --no-merges --pretty=format:"%h|%s"
```

**Get all tags** (for version detection):
```bash
git tag --list --sort=-version:refname
```

**Get commit count** (for version increment hint):
```bash
git rev-list --count $(git describe --tags --abbrev=0)..HEAD
```

**Check if commit is a merge**:
```bash
git rev-list --parents -n 1 <commit-hash> | grep -q " .* .*"
```

## Best Practices

1. **Prefer PR titles** over individual commits when available
2. **Group related changes** by feature or component
3. **Use user-facing language**, avoid technical jargon
4. **Skip internal commits** that don't affect users
5. **Combine granular commits** into cohesive changelog entries
6. **Link to issues/PRs** for detailed context
7. **Preserve intent**, even if wording changes

## Example Workflow

1. Get commits: `git log v1.0.0..HEAD --no-merges`
2. Parse each commit message
3. Classify by type (feat/fix/etc.)
4. Filter out internal commits
5. Group by scope or feature
6. Rephrase in user-facing language
7. Map to changelog sections
8. Deduplicate and clean up
9. Format as changelog entries
