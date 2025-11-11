---
description: Create a new README.md from scratch for projects without one
---

# Generate README

## Activated Agent

**Activate**: `readme-author` agent

The agent will help create a minimal, standards-compliant README for your project.

## Objective

Create a new README.md following the Personal minimal 8-section structure with business context integration and link-first approach.

## Command Parameters

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `--tier` | `prototype`, `mvp`, `production` | Auto-detect | Project maturity tier |
| `--format` | `console`, `markdown` | `console` | Output format (console display vs. file) |
| `--output` | `<path>` | `./README.md` | Custom output path (requires `--format=markdown`) |
| `--interactive` | `true`, `false` | `true` | Prompt for approval before writing |

**Examples:**
```bash
/document-generator:generate-readme                        # Interactive, auto-detect tier, console display
/document-generator:generate-readme --tier=mvp --format=markdown
/document-generator:generate-readme --output=./docs/README.md --format=markdown --interactive=false
```

## Activated Skills

The agent will activate these skills:

1. **`readme-authoring`** - 8-section templates and generation patterns
2. **`readme-standards`** -   minimal README validation criteria

## Process

The agent will follow this workflow:

### 1. Pre-flight Checks

**Check if README.md already exists**:
- If `README.md` exists in current directory:
  ```
  ⚠️  README.md already exists in this directory.

  Use `/document-generator:update-readme` to refactor an existing README.

  Do you want to:
  1. Overwrite the existing README (⚠️ this will replace current content)
  2. Cancel and use update-readme instead
  3. Generate to a different path

  Enter choice (1-3):
  ```
- If user chooses overwrite: Proceed with generation
- If user chooses cancel: Stop execution, suggest `/document-generator:update-readme`
- If user chooses different path: Prompt for new output path

### 2. Detect Project Tier

Agent will detect project tier (Prototype/MVP/Production) from codebase signals (if not specified via `--tier`). Display detected tier and allow user override if needed.

### 3. Extract Project Metadata

Agent will extract project name, version, and description from language-specific project files. If extraction fails, prompt user for required information.

### 4. Extract Business Context

Agent searches for business problem/solution in existing docs, module docstrings, and code comments. If not found, prompts user for business context (problem + solution). See `readme-authoring` skill "Context Extraction Patterns" for details.

### 5. Discover Existing Documentation

Agent scans for documentation to link (architecture, ADRs, setup guides, CONTRIBUTING.md). See `readme-authoring` skill "Documentation discovery" section for paths.

### 6. Generate 8-Section README

Generate content for all 8 sections using `readme-authoring` skill "Section Generation Reference" table:
- Title & One-Liner, Badges (tier-based), Description (with business context)
- Installation (simple command + setup link), Documentation (discovered links only)
- Supporting Components (optional), Contributing, Bugs & Enhancements

See `readme-authoring` skill for detailed generation patterns per section.

### 7. Present Draft (Interactive Mode)

If `--interactive=true` (default), show generated README to user:

```
📄 Generated README.md:

==================================================
# {Project Name}

{Generated content...}
==================================================

Sections included:
✓ Title & One-Liner
✓ Badges (MVP tier)
✓ Short Description (with business context)
✓ Installation
✓ Documentation (3 links)
✓ Contributing
✓ Bugs & Enhancements

Does this look good? (y/n/edit):
- y: Write to file
- n: Cancel generation
- edit: Modify specific sections
```

**If user chooses "edit"**:
```
Which section would you like to modify?
1. Title & One-Liner
2. Badges
3. Short Description
4. Installation
5. Documentation
6. Contributing
7. Bugs & Enhancements

Enter number (or 'done' to finish):
```

Allow user to provide replacement content for selected sections, then re-present draft.

### 8. Write README File

**Write to output path** (default: `./README.md`):

```bash
# Create README.md
cat > ./README.md <<'EOF'
{generated content}
EOF
```

**Confirm success**:
```
✓ README.md created successfully at ./README.md

Next steps:
- Review the README and adjust as needed
- Run `/document-generator:validate-readme` to check compliance
- Consider creating missing documentation linked in the README:
  - docs/architecture.md
  - docs/quickstart.md
```

**If `--format=console`** (display only):
- Show generated README in console
- Don't write file
- Provide copy-paste-ready output

## Output Format

Generate README following the 8-section minimal structure defined in `readme-authoring` skill.

**Example output** (Prototype tier):

```markdown
# Customer Churn Predictor

Early-stage prototype for predicting customer churn using transaction history.

## Description

The marketing team needs to identify customers at risk of churning to target retention campaigns effectively. This prototype implements a gradient boosting classifier trained on transaction and engagement data to predict churn probability. The model achieves 78% accuracy on historical data and provides interpretable feature importance for business teams.

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

## Constraints

- **Don't overwrite existing README** without explicit user confirmation
- **Only link to docs that exist** - verify files before adding links
- **Integrate business context** - don't create separate Business Problem/Solution sections
- **Keep it minimal** - 8 sections only, no extras
- **Respect tier** - Prototype gets minimal structure, Production gets comprehensive
- **No placeholder links** - if docs don't exist, note this instead of linking to empty files

## Error Handling

**No project metadata found**:
- Prompt user for project name and description
- Continue with manual input

**No business context found**:
- Prompt user for business problem/solution
- Don't skip this - it's required for Short Description

**No issue tracker detected**:
- Prompt user for issue tracker URL
- Provide example format

**Write permission denied**:
- Display error message
- Suggest alternative output path or check permissions

## Success Criteria

Generated README should:
- ✅ Follow 8-section minimal structure
- ✅ Include business problem/solution in Short Description
- ✅ Have actionable installation command
- ✅ Link to existing documentation (no placeholders)
- ✅ Be tier-appropriate (badges, documentation depth)
- ✅ Pass validation via `/document-generator:validate-readme`

## Related Commands

- **`/document-generator:validate-readme`** - Check README compliance
- **`/document-generator:update-readme`** - Refactor existing README
