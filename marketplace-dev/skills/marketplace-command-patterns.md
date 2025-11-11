---
title: Marketplace Command Patterns
description: Standard parameter patterns and output formatting for all marketplace commands
tags: [commands, parameters, output, user-interface]
---

# Marketplace Command Patterns

## Metadata

**Purpose**: Define standard command patterns for consistent user experience across marketplace
**Applies to**: All user-facing commands in marketplace plugins
**Version**: 1.0.0

---

## Instructions

### Standard Output Parameters

All user-facing commands in marketplace support:

**Format Parameter:**
- `--format=console` (default) - Display results in IDE/console
- `--format=markdown` - Generate markdown report file

**Output Parameter:**
- `--output=<path>` - Specify custom report file path
  - Only valid when `--format=markdown`
  - If not specified, uses default report path

**Default Report Paths:**
- Pattern: `./reports/{command-name}-report.md`
- Example: `./reports/validate-docs-report.md`

### Parameter Documentation Template

Include this section in every command file:

```markdown
## Command Parameters

This command supports the following optional parameters:

**Format Parameter:**
- `--format=console` (default) - Display results in IDE/console
- `--format=markdown` - Generate markdown report file

**Output Parameter:**
- `--output=<path>` - Specify custom report file path
  - Default: `./reports/{command-name}-report.md`
  - Only used with `--format=markdown`

**Usage Examples:**
\```bash
/{plugin-name}:{command-name}                                    # Console output
/{plugin-name}:{command-name} --format=markdown                  # Report in ./reports/
/{plugin-name}:{command-name} --format=markdown --output=./docs/report.md
\```
```

### Output Mode Implementation

**When `--format=console` (default):**
1. Display results directly in console/IDE
2. Use clear formatting for readability
3. Include summary statistics if applicable
4. Provide actionable recommendations

**When `--format=markdown`:**
1. Check if user specified `--output` parameter
   - If yes, use that path
   - If no, use default: `./reports/{command-name}-report.md`
2. Create report directory if it doesn't exist
3. Generate properly formatted markdown file with:
   - Metadata header (timestamp, project path, command used)
   - Executive summary
   - Detailed findings
   - Recommendations
   - Appendices (if applicable)
4. After saving:
   - Display confirmation with file path
   - Show brief summary in console

### Report File Structure

All markdown reports should follow this structure:

```markdown
# {Command Name} Report

**Generated**: {timestamp}
**Project**: {project-path}
**Command**: `/{plugin}:{command} {parameters}`

---

## Executive Summary

[High-level overview of findings, 2-3 sentences]

**Key Metrics**:
- Metric 1: Value
- Metric 2: Value

---

## Findings

### {Category 1}
[Detailed findings for category 1]

### {Category 2}
[Detailed findings for category 2]

---

## Recommendations

**High Priority**:
1. [Recommendation 1]
2. [Recommendation 2]

**Medium Priority**:
1. [Recommendation 3]

**Low Priority**:
1. [Recommendation 4]

---

## Appendices

### {Additional Details}
[Supporting information, raw data, etc.]
```

### Parameter Parsing Pattern

When implementing parameter handling in commands:

```markdown
## Parameter Detection

1. Check for `--format` parameter:
   - If `--format=markdown`, set output_mode to "markdown"
   - Otherwise, set output_mode to "console" (default)

2. Check for `--output` parameter (only if format=markdown):
   - If specified, use that path for report file
   - If not specified, use default: `./reports/{command-name}-report.md`
   - If format=console, ignore --output parameter

3. Validate parameters:
   - Warn if `--output` used without `--format=markdown`
   - Validate output path is writable
```

### Console Output Best Practices

**Structure:**
- Clear section headings
- Use tables for metrics/scores
- Use lists for findings/recommendations
- Use visual separators (---, ===)

**Tone:**
- Actionable and specific
- Avoid jargon where possible
- Provide context for recommendations

**Length:**
- Concise but complete
- Long details can go in markdown report

### Markdown Report Best Practices

**File Management:**
- Always create parent directories if missing
- Use consistent naming patterns
- Timestamp reports for versioning
- Overwrite existing report with same name (don't append)

**Formatting:**
- Use proper markdown hierarchy (# ## ###)
- Include code blocks with language specifiers
- Use tables for structured data
- Use blockquotes for important notes

**Content:**
- Self-contained (don't assume reader has console output)
- Include full context (project, command, timestamp)
- Provide actionable recommendations
- Link to relevant documentation/resources

---

## Resources

### Complete Command Implementation Example

```markdown
---
description: Validate documentation standards compliance
---

# Validate Documentation Command

You are a documentation standards validator for Personal.

## Command Parameters

This command supports the following optional parameters:

**Format Parameter:**
- `--format=console` (default) - Display results in IDE/console
- `--format=markdown` - Generate markdown report file

**Output Parameter:**
- `--output=<path>` - Specify custom report file path
  - Default: `./reports/validate-docs-report.md`
  - Only used with `--format=markdown`

**Usage Examples:**
\```bash
/validator:validate-docs                                    # Console output
/validator:validate-docs --format=markdown                  # Report in ./reports/
/validator:validate-docs --format=markdown --output=./docs/validation.md
\```

## Output Mode Instructions

### Step 1: Detect Output Mode

Parse command parameters to determine output mode:
- Check for `--format` parameter
- Check for `--output` parameter (if format=markdown)
- Set output_mode variable accordingly

### Step 2: Perform Analysis

[Execute validation logic here]

### Step 3: Format Output

**If output_mode is "console":**
1. Display results directly in console
2. Show summary, findings, recommendations
3. Use clear formatting for readability

**If output_mode is "markdown":**
1. Determine output path:
   - Use `--output` value if provided
   - Otherwise use `./reports/validate-docs-report.md`
2. Create report directory: `mkdir -p reports`
3. Generate markdown report with proper structure
4. Save to file using Write tool
5. Confirm to user: "Report saved to {path}"
6. Show brief summary in console

## Validation Process

1. Activate skill: `documentation-standards`
2. Scan repository for documentation files
3. Assess against standards
4. Calculate scores
5. Generate recommendations
6. Format output based on output_mode

## Output Format

[Specific format for this command's findings]
```

### Parameter Handling Code Pattern

When writing command instructions, include this pattern:

```markdown
## Parameter Handling

**Step 1: Parse parameters from user command**

Extract parameters from the command invocation:
- `--format=console` or `--format=markdown`
- `--output=<path>` (optional, only with markdown format)

**Step 2: Set defaults**

If no parameters specified:
- `output_mode = "console"`
- `output_path = null`

If `--format=markdown` but no `--output`:
- `output_path = "./reports/{command-name}-report.md"`

**Step 3: Validate**

- If `--output` specified without `--format=markdown`, warn user and ignore
- Ensure output path is valid (if specified)

**Step 4: Execute command**

Proceed with command logic, keeping output_mode in mind

**Step 5: Generate output**

Format results according to output_mode (console or markdown)
```
