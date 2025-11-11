---
description: Validate existing CHANGELOG.md against standards
---

# Validate Changelog

## Objective

Validate existing CHANGELOG.md against standards (Keep a Changelog format) and report compliance issues with severity levels.

## Activated Skills

1. **`changelog-standards`** (document-generator) - changelog format and structure
2. **`version-validation`** (document-generator) - Versioning rules and validation

## Parameters

- `--path` (optional): Changelog location (auto-detects if not specified)
- `--fix` (optional): Automatically fix common formatting issues
- `--output` (optional): `console` (default) or `markdown` (generate validation report)

## Process

### 1. Locate Changelog

Locate changelog file:
- If `--path` specified: Use that location
- Otherwise auto-detect from standard locations:
  - `CHANGELOG.md` (root)
  - `docs/CHANGELOG.md`
  - `docs/changelog/*.md` (yearly format)
  - Search for `**/CHANGELOG.md` or `**/changelog/*.md`

If not found:
```
❌ CHANGELOG.md not found

No changelog file detected in standard locations.

Run /document-generator:generate-changelog to create one.
```

### 2. Parse Changelog Structure

Read and extract:
- File header (title, preamble)
- [Unreleased] section
- Version entries with dates and tiers
- Changelog sections (Added, Changed, Fixed, etc.)
- Version comparison links

### 3. Validate Format

**Apply `changelog-standards` skill** to check:

#### Header Validation
- ✓ Has "# Changelog" or "# Change Log" title
- ✓ References Keep a Changelog format
- ⚠️ Missing header is a warning (not error)

#### Version Heading Validation
- ✓ Format: `## [VERSION] - YYYY-MM-DD` or `## [VERSION] - YYYY-MM-DD [TIER]`
- ❌ Missing brackets around version
- ❌ Incorrect date format (not YYYY-MM-DD)
- ⚠️ Invalid tier annotation

**Examples**:
```markdown
## [2.1.0] - 2025-11-01 [MVP]     ✓ Valid
## [2025.1] - 2025-01-15          ✓ Valid
## v2.1.0 - 2025-11-01             ❌ No brackets
## [2.1.0] - 11/01/2025            ❌ Wrong date format
## [2.1.0] - 2025-11-01 [Alpha]   ⚠️ Invalid tier (use Prototype)
```

#### Section Validation
- ✓ Uses standard sections (Added, Changed, Deprecated, Removed, Fixed, Security)
- ⚠️ Non-standard sections (Features, Bugs, etc.)
- ✓ Sections in correct order
- ⚠️ Empty sections (should remove or populate)

#### Link Validation
- ✓ Version comparison links at bottom
- ✓ Links follow format: `[VERSION]: URL`
- ⚠️ Missing links for versions
- ❌ Broken link format

### 4. Validate Versions

**Apply `version-validation` skill** to check:

#### Version Format
- ✓ Matches SemVer pattern (`X.Y.Z`)
- ✓ Matches CalVer pattern (`YYYY.N` or `YYYY.MM.N`)
- ❌ Invalid version format
- ⚠️ Mixed version types (both SemVer and CalVer)

#### Version Ordering
- ✓ Versions in reverse chronological order (newest first)
- ❌ Out-of-order versions
- ⚠️ Skipped versions (1.0.0 → 1.2.0, missing 1.1.0)

#### Version Increments
- ✓ Proper SemVer increments
- ✓ Proper CalVer increments
- ❌ Invalid increment (e.g., 2.1.5 → 2.3.0, skipped 2.2.x)

#### Date Validation
- ✓ Valid ISO dates (YYYY-MM-DD)
- ❌ Invalid date format
- ❌ Invalid date (e.g., Feb 30)
- ⚠️ Dates not in chronological order
- ⚠️ Future dates (minor warning)

### 5. Generate Validation Report

**Categorize issues** by severity:

**Errors** (❌) - Must fix:
- Invalid version format
- Invalid date format
- Out-of-order versions
- Broken heading structure

**Warnings** (⚠️) - Should fix:
- Missing tier annotations
- Skipped versions
- Non-standard sections
- Missing version links
- Empty sections

**Info** (ℹ️) - Nice to have:
- Missing header preamble
- Future dates
- Inconsistent formatting

**Output format** (console):
```
Validating CHANGELOG.md...

❌ Errors (3)
  Line 15: Invalid version format "v2.1.0" (should be "[2.1.0]")
  Line 23: Invalid date format "11/01/2025" (should be "YYYY-MM-DD")
  Line 30: Versions out of order ([1.5.0] before [2.0.0])

⚠️  Warnings (2)
  Line 42: Skipped version 1.1.0 (jumped from 1.0.0 to 1.2.0)
  Line 67: Non-standard section "Bugs" (use "Fixed")

ℹ️  Info (1)
  Missing version comparison links at bottom of file

Overall: Failed (3 errors, 2 warnings)
```

### 6. Auto-fix (if --fix enabled)

Automatically correct common issues:

**Fixable issues**:
- Add brackets around versions: `v2.1.0` → `[2.1.0]`
- Standardize date format: `11/01/2025` → `2025-11-01`
- Rename sections: `Bugs` → `Fixed`, `Features` → `Added`
- Add missing header preamble
- Generate version comparison links

**Not auto-fixable** (manual intervention required):
- Out-of-order versions (need reordering)
- Invalid dates (need manual correction)
- Skipped versions (intentional or error?)

**If --fix enabled**:
```
Fixing common issues...

✓ Fixed 5 issues automatically
  - Standardized 2 version formats
  - Corrected 2 date formats
  - Renamed 1 section

⚠️  2 issues require manual fix
  - Line 30: Reorder versions manually
  - Line 42: Confirm if version 1.1.0 was intentionally skipped

Updated CHANGELOG.md saved.
```

### 7. Output Results

**Console output** (default):
- Display validation summary
- List all errors and warnings with line numbers
- Provide fix suggestions
- Show overall pass/fail status

**Markdown report** (if `--output=markdown`):
- Save to `./reports/changelog-validation-report.md`
- Include all issues with context
- Link to changelog file
- Provide remediation steps

## Output Format

### Console (Default)

```
Validating CHANGELOG.md...

✓ Header present
✓ Keep a Changelog format referenced
✓ [Unreleased] section present
✓ 5 versions found

Checking versions...
  [2.1.0] ✓
  [2.0.0] ✓
  [1.5.0] ⚠️  Missing tier annotation
  [1.0.0] ✓

Checking format...
  ✓ All sections use standard names
  ✓ Versions in correct order
  ⚠️  2 versions missing comparison links

Summary:
- Errors: 0
- Warnings: 3
- Overall: Pass with warnings

Next steps:
1. Add tier annotations to versions
2. Generate comparison links at bottom
```

### Markdown Report (--output=markdown)

Same structure as console output above, saved to `./reports/changelog-validation-report.md` with:
- Full issue details with line numbers and context
- Fix recommendations for each issue
- Links to changelog file
- Remediation steps by priority

## Examples

**Basic validation**:
```bash
/document-generator:validate-changelog
→ Validates CHANGELOG.md and displays results in console
```

**Auto-fix issues**:
```bash
/document-generator:validate-changelog --fix
→ Validates and automatically fixes common formatting issues
```

**Generate report**:
```bash
/document-generator:validate-changelog --output=markdown
→ Saves validation report to ./reports/changelog-validation-report.md
```

**Combined**:
```bash
/document-generator:validate-changelog --fix --output=markdown
→ Fixes issues and generates report
```

**Custom location**:
```bash
/document-generator:validate-changelog --path=docs/CHANGELOG.md
→ Validates changelog at docs/CHANGELOG.md
```

## Constraints

- Token budget: Keep concise, delegate validation logic to skills
- Non-destructive by default (use --fix to modify)
- Preserve user content, only fix format
- Clear severity distinctions (error vs warning vs info)
