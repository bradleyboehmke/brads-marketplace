---
description: Review plugin components for redundancy, verbosity, and standards compliance
---

# Review Plugin Command

You are the **plugin-architect agent** performing a comprehensive quality review of a plugin or component.

## Command Parameters

This command supports the following parameters:

**Target Parameter:**
- `<plugin-path>` - Path to plugin directory, or specific component file
- Examples:
  - `./my-plugin` (review entire plugin)
  - `./my-plugin/commands/my-command.md` (review specific file)

**Format Parameter:**
- `--format=console` (default) - Display results in IDE/console
- `--format=markdown` - Generate markdown review report

**Output Parameter:**
- `--output=<path>` - Specify custom report file path
  - Default: `./reports/plugin-review-{plugin-name}.md`
  - Only used with `--format=markdown`

**Usage Examples:**
```bash
/marketplace-dev:review-plugin ./my-plugin                    # Review entire plugin
/marketplace-dev:review-plugin ./my-plugin/skills/my-skill.md # Review one file
/marketplace-dev:review-plugin ./my-plugin --format=markdown  # Generate report
```

## Objective

Review plugin components and identify opportunities for improvement in:
1. **Redundancy** - Duplicate content within and across components
2. **Verbosity** - Excessive or unclear content
3. **Standards Compliance** - Adherence to architecture principles
4. **Optimization** - Token efficiency improvements

## Activated Skills

- `plugin-architecture-principles` - Architecture standards
- `content-optimization-patterns` - Verbosity detection
- `plugin-structure-standards` - File structure requirements
- `marketplace-command-patterns` - Command pattern standards

## Review Process

### Step 1: Scope Detection

Determine what to review:
- If target is a directory: Review all agents, skills, commands in that plugin
- If target is a single file: Review that component only

Read all relevant files using the Read tool.

### Step 2: Redundancy Analysis

**Internal Redundancy** (within single file):
1. Search for repeated phrases or paragraphs
2. Identify duplicate examples
3. Check for restated concepts
4. Flag sections that could be consolidated

**Cross-Component Redundancy** (across multiple files):
1. Compare similar sections across files
2. Look for copy-pasted content
3. Identify duplicated templates or examples
4. Check if content should be extracted to shared skill

For each redundancy found, document:
- Location (file:line or file:section)
- Type (internal vs cross-component)
- Estimated token savings if removed
- Recommendation (consolidate, extract to skill, remove)

### Step 3: Verbosity Analysis

Reference `content-optimization-patterns` skill for detection patterns.

Check for:
1. **Redundant headers** - Multiple headers saying the same thing
2. **Repetitive phrasing** - "This command does...", "This skill provides..."
3. **Over-explained examples** - Long explanations for self-evident code
4. **Verbose instructions** - Run-on sentences instead of lists
5. **Unnecessary markers** - Excessive IMPORTANT/NOTE/WARNING tags
6. **Example bloat** - 10 examples of the same pattern
7. **Meta-commentary** - Transitional prose between sections

For each verbosity issue:
- Location (file:section)
- Pattern type (from content-optimization-patterns)
- Current length vs optimized length (token estimate)
- **Pros of reducing**: Token savings, clarity improvement
- **Cons of reducing**: Context loss risk, clarity reduction risk
- Recommendation with confidence level (High/Medium/Low)

### Step 4: Plugin Configuration Compliance (if target is a plugin)

**For plugin directories only:**

1. **Read `{plugin}/.claude-plugin/plugin.json`**
2. **Read `.claude-plugin/marketplace.json`** (marketplace root)

**Check plugin.json completeness:**
- Required fields present: name, description, version, author
- Description is clear and concise (not generic)
- Version follows semantic versioning (X.Y.Z)
- Tags are relevant and descriptive

**Check marketplace.json registration:**
- Plugin entry exists in marketplace.json
- Name matches: marketplace.json[name] = plugin.json[name]
- Description matches or is similar
- Source path is correct: `./{plugin-name}`
- Tags are consistent (marketplace subset of plugin tags)

For each issue:
- Configuration file (plugin.json or marketplace.json)
- Issue type (missing field, mismatch, incorrect value)
- Severity (Critical/High/Medium/Low)
- Recommendation

### Step 5: Standards Compliance

Reference `plugin-architecture-principles` for architecture standards.

Check component against:

**Size Guidelines**:
- Agent: < 500 lines
- Skill (instructions): < 400 lines
- Command: < 600 lines

**Architecture Principles**:
- Single responsibility (purpose in 5-10 words)
- No circular dependencies
- Clear agent vs skill vs command boundaries
- Skills use progressive disclosure (Metadata/Instructions/Resources)

**Anti-Patterns** (from plugin-architecture-principles):
- Kitchen Sink, Encyclopedia, Duplicate, Tangle, Orphan, Monolith Skill, Phantom Agent

**File Structure** (from plugin-structure-standards):
- Naming conventions (kebab-case, verb-focused for commands)
- Frontmatter present and complete
- Directory structure follows standard layout

For each violation:
- Standard violated
- Current state vs expected state
- Severity (Critical/High/Medium/Low)
- Recommendation

### Step 6: Generate Summary

Calculate total findings:
- Total redundancies (internal + cross-component)
- Total verbosity issues
- Total configuration issues (if plugin)
- Total standards violations
- Estimated total token savings
- Priority breakdown (Critical/High/Medium/Low)

## Output Format

### Console Output (--format=console)

Display review results in this structure:

```markdown
# Plugin Review: {plugin-name}

## Summary

**Components Reviewed**: {count}
**Total Findings**: {count}
- Redundancy: {count}
- Verbosity: {count}
- Configuration Issues: {count}
- Standards Violations: {count}

**Estimated Token Savings**: ~{X} tokens ({Y}% reduction)

---

## Configuration Issues ({count}) [if plugin]

1. **plugin.json** - {issue}
   - Severity: {level}
   - Current: {state}
   - Expected: {state}
   - Recommendation: {action}

2. **marketplace.json** - {issue}
   - Severity: {level}
   - Issue: {description}
   - Recommendation: {action}

---

## Redundancy Issues ({count})

### Internal Redundancy
1. **{file}**: {description}
   - Location: {section}
   - Savings: ~{X} tokens
   - Recommendation: {action}

### Cross-Component Redundancy
1. **{file1} + {file2}**: {description}
   - Savings: ~{X} tokens
   - Recommendation: Extract to skill `{skill-name}`

---

## Verbosity Issues ({count})

1. **{file}** - {pattern type}
   - Location: {section}
   - Savings: ~{X} tokens
   - **Pros**: {benefits of reducing}
   - **Cons**: {risks of reducing}
   - Confidence: {High/Medium/Low}

---

## Standards Violations ({count})

1. **{file}** - {standard}
   - Severity: {level}
   - Current: {state}
   - Expected: {state}
   - Recommendation: {action}

---

## Refactoring Recommendations

**High Priority** (Critical/High severity):
1. {recommendation}
2. {recommendation}

**Medium Priority**:
1. {recommendation}

**Low Priority** (optional improvements):
1. {recommendation}

---

## Next Steps

Would you like me to refactor this plugin based on these recommendations?
- Type 'yes' to proceed with automated refactoring
- Type 'selective' to choose which recommendations to apply
- Type 'no' to keep current state
```

### Markdown Report (--format=markdown)

Same structure as console, but saved to file with metadata header.

### Step 6: User Interaction

After presenting findings, ask:

> **Would you like me to refactor based on these recommendations?**
> - **yes**: Apply all High + Medium priority recommendations
> - **selective**: User chooses which to apply
> - **no**: Exit without changes

If user responds **yes**:
1. Apply recommendations in priority order
2. Update files using Edit/Write tools
3. Report changes made

If user responds **selective**:
1. Present recommendations one by one
2. Ask for confirmation on each
3. Apply only approved changes

If user responds **no**:
1. Confirm review complete
2. Remind user they can re-run command later
