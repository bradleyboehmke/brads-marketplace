---
description: Audit existing README.md compliance with   standards without making changes
---

# Validate README

## Activated Agent

**Activate**: `readme-author` agent

The agent will audit your README.md against Personal minimal standards.

## Objective

Validate existing README.md structure and content against   8-section minimal requirements, identify missing or incomplete sections, and provide actionable recommendations for improvement.

## Command Parameters

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `--tier` | `prototype`, `mvp`, `production` | Auto-detect | Project tier to validate against |
| `--format` | `console`, `markdown` | `console` | Output format (console display vs. report file) |
| `--output` | `<path>` | `./reports/readme-validation-report.md` | Custom report path (requires `--format=markdown`) |

**Examples:**
```bash
/document-generator:validate-readme                        # Console output, auto-detect tier
/document-generator:validate-readme --tier=mvp --format=markdown
/document-generator:validate-readme --format=markdown --output=./docs/readme-validation.md
```

## Activated Skills

The agent will activate these skills:

1. **`readme-standards`** -   minimal README validation criteria
2. **`readme-authoring`** - Reference templates for comparison

## Process

The agent will follow this workflow:

### 1. Pre-flight Checks

**Check if README.md exists**:
- If `README.md` not found in current directory:
  ```
  ❌ No README.md found in current directory.

  Use `/document-generator:generate-readme` to create one.

  Aborting validation.
  ```
  - Stop execution

- If `README.md` exists: Proceed with validation

### 2. Detect Project Tier

Agent will detect project tier (if not specified via `--tier`) and display for user. Validation will use tier-appropriate standards from `readme-standards` skill.

### 3. Parse README Structure

**Read and analyze README.md**:

1. **Extract sections** - Identify which of the 8 sections are present (with flexible section names):
   - Title & One-Liner (check for `# {Title}` and description)
   - Badges Block (check for shield.io badges or similar)
   - Short Description (`## Description` or `## Overview` acceptable)
   - Installation (`## Installation` or `## Quick Start`)
   - Documentation (dedicated `## Documentation` section OR links within `## Guides`/other sections)
   - Supporting Components (`## Supporting Components`)
   - Contributing (dedicated `## Contributing` section OR link within `## Documentation`/`## Guides`)
   - Issue Reporting (dedicated `## Bugs` section OR link within `## Contributing`/`## Documentation`)

2. **Check heading hierarchy**:
   - Title uses `#`
   - Sections use `##`
   - No `###` headings (keep it minimal)

3. **Count sections** - Track which required vs. optional sections are present

### 4. Validate Content Quality

For each section, validate content:

**Title & One-Liner** (REQUIRED):
- ✅ Level 1 heading present
- ✅ One-liner present (1-2 sentences)
- ✅ Description is specific, not vague
- ⚠️ If missing or vague: Flag as incomplete

**Badges** (OPTIONAL, tier-dependent):
- ℹ️ Note if missing for MVP/Production projects
- ✅ If present, check format (shields.io or similar)
- ⚠️ If placeholder badges: Flag as incomplete

**Short Description** (REQUIRED):
- ✅ `## Description` or `## Overview` heading present
- ✅ Paragraph length appropriate (3-5 sentences)
- ✅ **Business problem context** included
- ✅ **Solution context** included
- ℹ️ Separate `## Business Problem` or `## Solution` sections acceptable if brief and focused
- ✅ Preferred approach: Integrate business/solution context into single Description/Overview paragraph
- ⚠️ If business context missing: Flag as incomplete

**Installation** (REQUIRED):
- ✅ `## Installation` heading present
- ✅ Installation command in code block
- ✅ Command is actionable (not "install this project")
- ✅ Link to setup guide if `docs/setup.md` exists
- ⚠️ If missing link to existing setup guide: Flag as incomplete

**Documentation** (REQUIRED):
- ✅ Documentation links present (can be in dedicated `## Documentation` section OR within `## Guides` or similar section)
- ✅ At least one documentation link provided
- ✅ Links point to existing files (validate)
- ⚠️ If ADRs exist in `adr/` but not linked anywhere: Recommend linking
- ⚠️ If architecture docs exist but not linked anywhere: Recommend linking
- ⚠️ If minimal documentation: Suggest additions

**Supporting Components** (OPTIONAL):
- ℹ️ Note if missing (not an error)
- ✅ If present, lists actual dependencies with links

**Contributing Link** (REQUIRED):
- ✅ Contributing guidance or link present (can be dedicated `## Contributing` section OR link within `## Documentation`/`## Guides`)
- ✅ Link to `CONTRIBUTING.md` if file exists (can be in any section)
- ✅ If no `CONTRIBUTING.md`, basic guidance provided somewhere in README
- ⚠️ If `CONTRIBUTING.md` exists but not linked anywhere: Recommend linking
- ⚠️ If MVP/Production without `CONTRIBUTING.md`: Suggest creating one

**Issue Reporting** (REQUIRED):
- ✅ Issue reporting link or guidance present (can be dedicated `## Bugs` section OR link within `## Contributing`/`## Documentation`)
- ✅ Issue tracker link provided somewhere in README
- ⚠️ If no clear path to report issues: Flag as missing

### 5. Validate Links

**Check documentation links** referenced in README:

1. **Relative links** - Verify files exist:
   - `docs/setup.md`
   - `docs/architecture.md`
   - `adr/`
   - `CONTRIBUTING.md`

2. **External links** - Note but don't verify (assume valid):
   - GitHub Issues URLs
   - API documentation URLs
   - Confluence links

3. **Flag broken links**:
   ```
   ❌ Broken link: docs/quickstart.md (file not found)
   ```

### 6. Check for Undiscovered Documentation

**Scan for documentation not linked in README**:

```bash
# Check for common doc files
test -f docs/architecture.md && echo "Architecture doc exists"
test -d adr && echo "ADRs exist"
test -f CONTRIBUTING.md && echo "Contributing guide exists"
```

**If documentation exists but not linked**:
```
⚠️  Found documentation not linked in README:
   - docs/architecture.md exists but not linked in Documentation section
   - adr/ exists (3 ADRs) but not linked
```

### 7. Generate Compliance Report

**Tier-appropriate validation** using `readme-standards` skill criteria.

**Calculate compliance score**:
- Count required content present (out of 6 core requirements: Title, Description/Overview, Installation, Documentation links, Contributing link, Issue reporting)
- Note: Section names can vary - focus on whether essential content/links exist somewhere in README
- Count optional sections present (out of 2: Badges, Supporting Components)
- Count content quality issues (missing business context, broken links, etc.)

**Assign compliance level**:
- ✅✅✅ **Excellent** - All required content present, business context clear, comprehensive links, tier-appropriate
- ✅✅ **Standard** - All required content present, minor content gaps
- ✅ **Minimal** - Required content mostly present, some significant gaps (missing contributing link or issue reporting)
- ❌ **Non-compliant** - Missing multiple core requirements

### 8. Present Results

**Console format** (`--format=console`, default):

```
📋 README Validation Report

Project: {Project Name}
Tier: {Detected Tier}
Compliance Level: ✅✅ Standard

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✅ COMPLIANT SECTIONS (5/6 required, 1/2 optional)

1. Title & One-Liner - Clear and descriptive
2. Short Description - Business context included
3. Installation - Simple command with setup link
4. Documentation - 3 resources linked
5. Bugs & Enhancements - Issue tracker linked

ℹ️  OPTIONAL SECTIONS

6. Badges - Not present (MVP tier - recommended)
7. Supporting Components - Not applicable

⚠️  INCOMPLETE SECTIONS (1)

8. Contributing - Section present but CONTRIBUTING.md not linked
   → CONTRIBUTING.md exists at ./CONTRIBUTING.md
   → Add link in Contributing section

❌ MISSING SECTIONS (1)

9. (None)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📌 RECOMMENDATIONS

Priority 1 (Required):
- Link to CONTRIBUTING.md in Contributing section

Priority 2 (Suggested):
- Add badges (project is MVP tier - version, lifecycle, docs, code style)
- Link to ADRs in Documentation section (3 ADRs found in adr/)

Priority 3 (Optional):
- Create quickstart guide (docs/quickstart.md)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

✨ NEXT STEPS

Run `/document-generator:update-readme` to automatically fix issues.
```

**Markdown format** (`--format=markdown`):

Generate detailed report using structure from `readme-standards` skill Resources section.

Write to output path (default: `./reports/readme-validation-report.md`):

```markdown
# README Validation Report

**Project**: {Project Name}
**Date**: {Date}
**Tier**: {Detected Tier}
**Compliance Level**: ✅✅ Standard

## Summary

- ✅ 5 of 6 required sections compliant
- ⚠️ 1 section incomplete
- ❌ 0 sections missing
- ℹ️ 1 of 2 optional sections present

## Detailed Assessment

### ✅ Compliant Sections

1. **Title & One-Liner** - Clear and descriptive
   - Title: "Customer Segmentation Engine"
   - One-liner present and specific

2. **Short Description** - Business context included
   - Business problem: Marketing teams need customer segmentation
   - Solution: Clustering service for targeted campaigns
   - Core functionality described

...

### ⚠️ Incomplete Sections

8. **Contributing** - Section present but incomplete
   - Section exists with basic guidance
   - CONTRIBUTING.md exists at `./CONTRIBUTING.md` but not linked
   - **Recommendation**: Add link to CONTRIBUTING.md

### ❌ Missing Sections

(None)

## Recommendations

### Priority 1 (Required)
- Link to CONTRIBUTING.md in Contributing section

### Priority 2 (Suggested)
- Add badges (MVP tier: version, lifecycle, docs, code style)
- Link to ADRs in Documentation section

### Priority 3 (Optional)
- Create quickstart guide

## Next Steps

Run `/document-generator:update-readme` to automatically fix issues.
```

**Create reports directory if needed**:
```bash
mkdir -p reports
```

**Confirm report creation**:
```
✓ Validation report saved to ./reports/readme-validation-report.md
```

## Output Format

**Console output** - Structured, scannable report with emojis for visual clarity

**Markdown report** - Detailed, archivable document following structure from `readme-standards` skill

## Validation Levels

Using progressive validation from `readme-standards` skill:

**Level 1: Structure** (must pass for minimal compliance):
- All 6 required pieces of content present (title, description/overview, installation, docs links, contributing link, issue reporting)
- Section names can vary - essential content matters more than exact section structure
- Proper heading hierarchy

**Level 2: Content** (standard compliance):
- Business problem/solution context included (in Description, Overview, or separate sections)
- Actionable installation command
- Valid documentation links
- Contributing guidance accessible (dedicated section or link within docs/guides)
- Issue reporting path clear (dedicated section or link within contributing/docs)

**Level 3: Quality** (excellent compliance):
- Tier-appropriate badges
- Comprehensive documentation links (architecture, ADRs, guides)
- CONTRIBUTING.md exists and linked for mature projects
- All available documentation linked appropriately

## Constraints

- **Read-only** - This command does not modify README.md
- **Link validation** - Only check relative links, not external URLs
- **Tier-appropriate** - Validation criteria adjust based on project tier
- **No speculation** - Only flag issues based on actual file checks
- **Actionable recommendations** - Every issue should have clear fix

## Error Handling

**README.md not found**:
- Display clear error message
- Suggest using `/document-generator:generate-readme`
- Stop execution

**Cannot create reports directory**:
- Display error with permission issue
- Suggest alternative output path

**README.md unreadable**:
- Display error (encoding issue, permissions)
- Suggest checking file permissions

## Success Criteria

Validation report should:
- ✅ Accurately identify missing/incomplete sections
- ✅ Provide tier-appropriate recommendations
- ✅ Flag broken links and missing doc references
- ✅ Give clear, actionable next steps
- ✅ Assign appropriate compliance level

## Related Commands

- **`/document-generator:generate-readme`** - Create new README
- **`/document-generator:update-readme`** - Fix identified issues
