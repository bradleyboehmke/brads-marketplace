---
description: Verify and update marketplace documentation for plugins, agents, commands, and skills
---

# Update Plugin Documentation Command

You are a **documentation specialist** ensuring marketplace plugin documentation stays synchronized with the codebase.

## Command Parameters

**Target Parameter:**
- `<target-path>` - Path to plugin directory or specific component file
- Examples:
  - `./marketplace-dev` (entire plugin)
  - `./marketplace-dev/commands/review-plugin.md` (specific command)
  - `./marketplace-dev/skills/content-optimization-patterns.md` (specific skill)
  - `./marketplace-dev/agents/plugin-architect.md` (specific agent)

**Usage Examples:**
```bash
/marketplace-dev:update-plugin-docs ./marketplace-dev
/marketplace-dev:update-plugin-docs ./marketplace-dev/commands/review-plugin.md
/marketplace-dev:update-plugin-docs ./validator/skills/documentation-standards.md
```

## Objective

Verify that plugins, agents, commands, and skills are properly documented in the marketplace documentation:
- `docs/architecture.md` - Architecture overview and examples
- `docs/usage.md` - Usage examples and workflows
- `docs/capabilities/plugins.md` - Plugin catalog
- `docs/capabilities/agents.md` - Agent catalog
- `docs/capabilities/commands.md` - Command reference
- `docs/capabilities/skills.md` - Skills catalog

If documentation is missing or outdated, offer to update it.

## Process

### Step 1: Analyze Target

Determine what type of component is being documented:

**If target is a directory** (plugin):
1. Read `plugin.json` for plugin metadata
2. List all agents in `agents/` directory
3. List all skills in `skills/` directory
4. List all commands in `commands/` directory
5. Extract descriptions from frontmatter of each component

**If target is a file** (agent/skill/command):
1. Determine component type from path:
   - `agents/*.md` → Agent
   - `skills/*.md` → Skill
   - `commands/*.md` → Command
2. Read frontmatter for description
3. Identify parent plugin from directory structure

### Step 2: Extract Component Information

For each component, gather:
- **Plugin**: name, description, version, tags (from `plugin.json`)
- **Agent**: name, description, primary role (from frontmatter + content)
- **Skill**: name (title), description, key knowledge areas (from frontmatter)
- **Command**: name, description, typical time, output type (from frontmatter + content)

### Step 2.5: Verify Plugin Registration (if target is a plugin)

**For plugin directories, check configuration consistency:**

1. **Read `.claude-plugin/marketplace.json`** (marketplace root)
2. **Read `{plugin}/.claude-plugin/plugin.json`**

**Verify consistency:**
- `marketplace.json` → plugin entry exists
- `marketplace.json[name]` = `plugin.json[name]`
- `marketplace.json[description]` = `plugin.json[description]` (or close match)
- `marketplace.json[source]` points to correct directory (`./{plugin-name}`)
- `marketplace.json[tags]` subset of `plugin.json[tags]` (if both exist)

**Document findings:**
- Plugin not registered in marketplace.json
- Name mismatch between files
- Description mismatch between files
- Incorrect source path
- Tags inconsistency

### Step 3: Verify Documentation

Read the relevant documentation files and check for presence:

**For Plugins:**
- `docs/capabilities/plugins.md` - Check "Available Plugins" table for entry
- `docs/usage.md` - Check "Available Plugins" table for entry
- `docs/architecture.md` (optional) - May have examples if plugin is foundational

**For Agents:**
- `docs/capabilities/agents.md` - Check "Available Agents" table for entry
- `docs/architecture.md` - May be referenced in examples

**For Skills:**
- `docs/capabilities/skills.md` - Check appropriate plugin section for entry

**For Commands:**
- `docs/capabilities/commands.md` - Check plugin section for entry
- `docs/usage.md` - Check "Quick Reference" table and workflow examples

For each documentation file, verify:
1. **Presence** - Is component mentioned?
2. **Accuracy** - Does description match current implementation?
3. **Completeness** - Are all metadata fields populated?

Document findings:
- Missing entries
- Outdated descriptions
- Incomplete information

### Step 4: Present Findings

Display verification results to user:

```markdown
# Documentation Verification: {component-name}

## Component Information

**Type**: {Plugin/Agent/Skill/Command}
**Plugin**: {plugin-name}
**Description**: {current-description}

---

## Plugin Registration Status (for plugins only)

### .claude-plugin/marketplace.json
- **Status**: {✅ Registered / ❌ Not registered}
- **Name Match**: {✅ Consistent / ⚠️ Mismatch: marketplace=X, plugin.json=Y}
- **Description Match**: {✅ Consistent / ⚠️ Different}
- **Source Path**: {✅ Correct / ⚠️ Incorrect: should be ./{plugin-name}}
- **Tags**: {✅ Consistent / ⚠️ Mismatch or missing}

---

## Documentation Status

### docs/capabilities/plugins.md
- **Status**: {✅ Present and current / ⚠️ Outdated / ❌ Missing}
- **Issue**: {description if not current}

### docs/capabilities/agents.md
- **Status**: {✅ Present and current / ⚠️ Outdated / ❌ Missing}
- **Issue**: {description if not current}

### docs/capabilities/skills.md
- **Status**: {✅ Present and current / ⚠️ Outdated / ❌ Missing}
- **Issue**: {description if not current}

### docs/capabilities/commands.md
- **Status**: {✅ Present and current / ⚠️ Outdated / ❌ Missing}
- **Issue**: {description if not current}

### docs/usage.md
- **Status**: {✅ Present and current / ⚠️ Outdated / ❌ Missing}
- **Issue**: {description if not current}

### docs/architecture.md
- **Status**: {✅ Referenced / - Not applicable / ❌ Should be referenced}
- **Issue**: {description if should be added}

---

## Summary

**Total Issues**: {count}
- Missing: {count}
- Outdated: {count}
- Incomplete: {count}
```

### Step 5: User Interaction

After presenting findings, ask:

> **Would you like me to update the documentation to fix these issues?**
> - Type **yes** to update all documentation
> - Type **no** to skip updates

If user responds **yes**:
1. Update each file using Edit tool
2. Add missing entries in appropriate locations
3. Update outdated descriptions
4. Ensure consistent formatting
5. Report changes made

If user responds **no**:
1. Confirm documentation review complete
2. Remind user they can re-run command later

### Step 6: Post-Update Reminder

After updates (whether user accepted or declined), display reminder:

> **Note**: If you made significant updates to the plugin structure:
> - Consider updating the architecture diagram: `/document-generator:generate-architecture-diagram`
> - The full repository architecture is documented in `docs/full-repo-architecture.md`
> - Run this command to regenerate the Mermaid diagram showing all plugins, agents, skills, and commands

## Update Patterns

### Adding Plugin to docs/capabilities/plugins.md

Add to "Available Plugins" table:
```markdown
| **{plugin-name}** | {description} | {command-list} |
```

### Adding Agent to docs/capabilities/agents.md

Add to "Available Agents" table:
```markdown
| **`{agent-name}`** | {plugin-name} | {description} | {primary-role} |
```

### Adding Skill to docs/capabilities/skills.md

Add to appropriate plugin section:
```markdown
| **`{skill-name}`** | {description} | {key-knowledge} |
```

### Adding Command to docs/capabilities/commands.md

Add to appropriate plugin section:
```markdown
| `/{plugin}:{command}` | {description} | {time} | {output} |
```

And add usage example:
```markdown
**Common Usage:**
\```bash
/{plugin}:{command}
/{plugin}:{command} --format=markdown
\```
```

### Adding to docs/usage.md

Add to "Quick Reference" table:
```markdown
| `/{plugin}:{command}` | {purpose} | {time} | {output} |
```

And optionally add to workflow examples if command is commonly used.
