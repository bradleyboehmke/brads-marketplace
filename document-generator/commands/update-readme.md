---
description: Refactor existing README.md to conform to   standards
---

# Update README

## Activated Agent

**Activate**: `readme-author` agent

The agent will refactor your existing README.md to meet Personal minimal standards.

## Objective

Update existing README.md to conform to   8-section minimal structure, preserving compliant content while adding missing sections and integrating business context.

## Command Parameters

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `--sections` | Comma-separated: `title`, `badges`, `description`, `installation`, `documentation`, `components`, `contributing`, `bugs` | All missing/incomplete | Specific sections to update |
| `--tier` | `prototype`, `mvp`, `production` | Auto-detect | Target project tier |
| `--format` | `console`, `markdown` | `console` | Output format (console display vs. write file) |
| `--output` | `<path>` | `./README.md` | Output path (use different path to preserve original) |
| `--interactive` | `true`, `false` | `true` | Show diffs and prompt for approval |

**Examples:**
```bash
/document-generator:update-readme                                      # Interactive, all sections
/document-generator:update-readme --sections=description,documentation
/document-generator:update-readme --tier=mvp --format=markdown --interactive=false
/document-generator:update-readme --output=./README-new.md --format=markdown
```

## Activated Skills

The agent will activate these skills:

1. **`readme-authoring`** - Templates for missing sections
2. **`readme-standards`** - Validation criteria and compliance checking

## Process

The agent will follow this workflow:

### 1. Pre-flight Checks

**Check if README.md exists**:
- If `README.md` not found:
  ```
  ❌ No README.md found in current directory.

  Use `/document-generator:generate-readme` to create one.

  Aborting update.
  ```
  - Stop execution

**Create backup** (before making changes):
```bash
cp README.md README.md.backup
```

Notify user:
```
📁 Backup created: README.md.backup
```

### 2. Validate Current README

**Run validation first** (same logic as `validate-readme`):
- Parse structure
- Identify missing/incomplete sections
- Check content quality
- Validate links

**Display current state**:
```
📊 Current README Status

Tier: MVP (detected)
Compliance: ✅ Minimal

Issues found:
⚠️  1. Short Description - Missing business problem context
⚠️  2. Documentation - ADRs not linked (adr/ exists)
❌ 3. Contributing - Section missing
ℹ️  4. Badges - Not present (recommended for MVP tier)

Ready to fix these issues.
```

### 3. Determine Sections to Update

**If `--sections` parameter provided**:
- Only update specified sections
- Skip sections not in the list

**If no `--sections` parameter**:
- Update all missing sections (❌)
- Update all incomplete sections (⚠️)
- Note optional sections (ℹ️) but don't auto-add unless requested

**Priority order**:
1. Missing required sections (Contributing, Installation, etc.)
2. Incomplete sections (missing business context, broken links)
3. Optional enhancements (Badges, Supporting Components)

### 4. Extract Context for Updates

Same extraction logic as `generate-readme`:

**For missing/incomplete sections, gather**:
- Project metadata (from pyproject.toml, package.json, etc.)
- Business context (from docs, code, or user input)
- Existing documentation to link
- Issue tracker URL
- CONTRIBUTING.md location

**Preserve existing content**:
- Don't regenerate compliant sections
- Extract and reuse content from non-compliant sections
- Maintain user's formatting choices where possible

### 5. Generate Section Updates

For each section needing update:

**Title & One-Liner**:
- Preserve existing title if present
- Add one-liner if missing
- Improve vague descriptions

**Badges** (if missing and tier >= MVP):
- Generate minimal badge set
- Insert after title, before description

**Short Description**:
- **If "## Overview" exists instead of "## Description"**:
  - Keep as "## Overview" (both acceptable per standards)
  - Only update if content lacks business context

- **If separate "Business Problem" and "Solution" sections exist**:
  - Note: This is acceptable per flexible standards
  - Offer to merge into single `## Description` or `## Overview` paragraph for conciseness (optional)
  - If user prefers merged format: Extract, merge, show diff
  - If user prefers separate: Keep as-is if content is brief and focused

- **If description/overview lacks business context**:
  - Prompt user for business problem/solution
  - Integrate into existing description or overview
  - Preserve technical details

**Installation**:
- If missing: Generate from project type
- If incomplete: Add link to setup guide if exists
- If overly detailed: Suggest moving to docs/setup.md

**Documentation**:
- Check if docs are in dedicated `## Documentation` section OR within `## Guides` or similar
- Add links to discovered docs not currently linked (anywhere in README)
- If docs scattered across multiple sections, offer to consolidate (optional)
- Verify all existing links still valid
- Organize in logical order (Quickstart, API, Architecture, ADRs)

**Supporting Components**:
- Only add if dependencies detected
- Skip if standalone project

**Contributing**:
- Check if contributing link exists in dedicated `## Contributing` section OR within `## Documentation`/`## Guides`
- If CONTRIBUTING.md exists but not linked anywhere: Add link (in existing docs section or create new Contributing section)
- If no CONTRIBUTING.md: Offer to create basic Contributing section with inline guidance
- Add test command if detectable

**Issue Reporting**:
- Check if issue reporting exists in dedicated `## Bugs` section OR within `## Contributing`/`## Documentation`
- If missing anywhere: Add link (in existing section or create new Bugs section)
- GitHub Issues link if GitHub repo detected
- Prompt user for issue tracker if not detectable

### 6. Present Diffs (Interactive Mode)

For each section being updated, show before/after diff:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
UPDATE: Short Description
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

BEFORE:
────────────────────────────────────────────────
## Business Problem
Marketing teams struggle with customer segmentation.

## Solution
This tool provides automated clustering.

## Description
The Customer Segmentation Engine uses ML to group customers.
────────────────────────────────────────────────

AFTER:
────────────────────────────────────────────────
## Description

Marketing teams struggle with customer segmentation, leading to ineffective campaign targeting and low conversion rates. This tool provides automated clustering capabilities using machine learning to group customers by purchasing behavior. The Customer Segmentation Engine processes transaction history and demographic data to generate actionable segments for targeted marketing campaigns.
────────────────────────────────────────────────

Changes:
- Merged Business Problem and Solution sections into Description
- Integrated business context into cohesive paragraph
- Preserved technical details from original Description

Apply this update? (y/n/edit):
```

**User options**:
- `y`: Apply this update
- `n`: Skip this update
- `edit`: Modify the generated content before applying
- `all`: Apply all remaining updates without prompting

**If user chooses "edit"**:
```
Enter updated content for Short Description:
(Paste content, then press Ctrl+D or type 'done' on new line)

> ___
```

Accept user's edited content and continue.

### 7. Apply Updates

**Build updated README**:

1. Start with existing README content
2. For each section to update:
   - If section exists: Replace content
   - If section missing: Insert in correct position (maintain 8-section order)
   - If section needs removal (e.g., separate Business Problem): Remove it

3. Maintain proper structure:
   - Title first (`#`)
   - Badges after title (if present)
   - Sections in order (`##`)
   - Preserve custom sections not in standard 8 (at end)

**Example transformation**:

**Before (non-compliant)**:
```markdown
# My Project

## Business Problem
Teams have issues.

## Solution
This fixes it.

## Setup
Install stuff.
```

**After (compliant)**:
```markdown
# My Project

Brief description of what this does and why.

## Description

Teams struggle with X problem, leading to Y consequence. This project provides Z solution by implementing W approach. The system handles A, B, and C use cases.

## Installation

\`\`\`bash
pip install my-project
\`\`\`

## Documentation

- [Architecture](docs/architecture.md) - System design
- [ADRs](adr/) - Key decisions

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Bugs & Enhancements

Report issues via [GitHub Issues](https://github.com/org/my-project/issues).
```

### 8. Write Updated README

**If `--format=markdown`** (write file):

```bash
# Write updated README
cat > ./README.md <<'EOF'
{updated content}
EOF
```

**Confirm success**:
```
✓ README.md updated successfully

Sections updated:
  1. Short Description - Merged Business Problem/Solution, added context
  2. Documentation - Added links to ADRs and architecture docs
  3. Contributing - Added link to CONTRIBUTING.md

Backup saved to: README.md.backup

Next steps:
- Review the updated README
- Run `/document-generator:validate-readme` to verify compliance
- Consider creating suggested documentation:
  - docs/quickstart.md
```

**If `--format=console`** (display only):
- Show full updated README
- Don't write file
- Note that backup was NOT created (no changes made)

### 9. Cleanup

**If changes were successfully applied**:
- Keep backup file (README.md.backup)
- User can delete backup later

**If user cancelled**:
- Remove backup file
- Leave original README unchanged

## Interactive Patterns

### Prompt for Business Context

If description lacks business problem/solution:

```
The Short Description section is missing business context.

To update it, I need to know:

1. What business problem does this project solve?
   (1-2 sentences describing the problem and its impact)

   > ___

2. What solution does this project provide?
   (1-2 sentences describing how it addresses the problem)

   > ___
```

### Confirm Major Changes

For significant restructuring (merging sections, removing content):

```
⚠️  Major Restructure Detected

This update will:
- Merge "Business Problem" and "Solution" sections into "Description"
- Remove separate sections (content will be preserved)
- Add 2 new sections (Contributing, Bugs & Enhancements)

This is a significant change. Continue? (y/n):
```

### Handle Custom Sections

If README has custom sections beyond the standard 8:

```
ℹ️  Custom Sections Detected

Your README contains custom sections:
- ## FAQ
- ## Troubleshooting
- ## Changelog

These will be preserved at the end of the README.

Continue? (y/n):
```

## Constraints

- **Preserve compliant content** - Don't regenerate sections that meet standards
- **Maintain user intent** - Keep custom sections, preserve formatting preferences
- **Show diffs for transparency** - User should see all changes before applying
- **Create backups** - Always backup before modifying
- **Link validation** - Only add links to docs that actually exist
- **Respect tier** - Apply tier-appropriate standards

## Error Handling

**README.md not found**:
- Suggest using `generate-readme`
- Stop execution

**README.md not writable**:
- Check file permissions
- Suggest alternative output path

**Backup creation fails**:
- Warn user
- Prompt to continue without backup or cancel

**User cancels mid-update**:
- Restore from backup
- Clean up partial changes

## Success Criteria

Updated README should:
- ✅ Preserve all compliant existing content
- ✅ Fix identified compliance issues
- ✅ Integrate business context into Description
- ✅ Link to all discovered documentation
- ✅ Follow 8-section minimal structure
- ✅ Pass validation via `/document-generator:validate-readme`

## Special Cases

### Optional: Merging Business Problem/Solution Sections

**Note**: Per updated standards, separate Business Problem/Solution sections are acceptable if brief and focused.

**If README has** separate sections and user prefers merged format:
```markdown
## Business Problem
{problem text}

## Solution
{solution text}

## Description
{technical details}
```

**Offer to transform to** (optional):
```markdown
## Description

{problem text}. {solution text}. {technical details}.
```

**Or keep as-is** if user prefers separate sections (compliant per flexible standards)

### Handling Overly Detailed Installation

**If Installation section has**:
```markdown
## Installation

1. Install Python 3.9+
2. Create virtual environment
3. Install dependencies: pip install -r requirements.txt
4. Set up database: ...
5. Run migrations: ...
6. Configure environment: ...
```

**Suggest**:
```
⚠️  Installation section is overly detailed.

Recommendation: Move detailed setup to docs/setup.md

Updated Installation section:
───────────────────────────────────────
## Installation

\`\`\`bash
pip install my-project
\`\`\`

For detailed setup and configuration, see [Setup Guide](docs/setup.md).
───────────────────────────────────────

Apply this simplification? (y/n):
```

### Preserving Custom Content

If README has unique sections (FAQ, Roadmap, Changelog):
- Keep them at the end of README
- Maintain their order
- Don't flag as non-compliant
- Note in update summary

## Related Commands

- **`/document-generator:validate-readme`** - Check README before/after update
- **`/document-generator:generate-readme`** - Create new README instead

## Batch Update Mode

**For non-interactive batch updates** (`--interactive=false`):

- Apply all fixes automatically
- No user prompts
- Create detailed update log
- Save to `./reports/readme-update-log.md`

**Use with caution** - Review changes carefully after batch update.
