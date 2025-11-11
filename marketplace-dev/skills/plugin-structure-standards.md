---
title: Plugin Structure Standards
description: File structure, naming conventions, and frontmatter requirements for marketplace plugins
tags: [structure, naming, frontmatter, conventions]
---

# Plugin Structure Standards

## Metadata

**Purpose**: Define file structure and naming conventions for marketplace plugins
**Applies to**: All Personal marketplace plugins
**Version**: 1.0.0

---

## Instructions

### Plugin Naming Conventions

**Plugin Directory Names**:
- Use kebab-case: `marketplace-dev`, `repo-investigator`
- Be descriptive but concise
- Avoid redundant "plugin" suffix

**Plugin Names in plugin.json**:
- Match directory name exactly
- Used in marketplace.json registration
- Used in command namespace (e.g., `/plugin-name:command`)

### Required Files

Every plugin MUST have:
1. **`.claude-plugin/plugin.json`** - Plugin metadata
2. **At least one**: Agent OR Command

**plugin.json Structure**:
```json
{
  "name": "plugin-name",
  "description": "Clear 5-10 word description",
  "version": "X.Y.Z",
  "author": {
    "name": "Personal Team"
  },
  "tags": ["relevant", "searchable", "tags"]
}
```

### Directory Structure

**Standard Layout**:
```
plugin-name/
├── .claude-plugin/
│   └── plugin.json          # Required
├── agents/                   # Optional
│   └── expert-name.md
├── skills/                   # Optional
│   ├── knowledge-area-1.md
│   └── knowledge-area-2.md
└── commands/                 # Optional
    ├── action-1.md
    └── action-2.md
```

**Personal**:
- All plugin development docs go in root `README.md`
- No nested plugin directories
- Flat structure within each component type

### File Naming Conventions

**Agents**: `{role}-{specialty}.md`
- Examples: `plugin-architect.md`, `documentation-validator.md`
- Lowercase, kebab-case
- Descriptive of expertise

**Skills**: `{domain}-{topic}.md`
- Examples: `plugin-architecture-principles.md`, `progressive-disclosure.md`
- Lowercase, kebab-case
- Noun-focused

**Commands**: `{action}-{target}.md`
- Examples: `validate-docs.md`, `design-plugin.md`
- Lowercase, kebab-case
- Verb-focused

### Frontmatter Requirements

**All component files** must have YAML frontmatter:

**Agents**:
```yaml
---
description: Brief description of agent expertise
---
```

**Skills**:
```yaml
---
title: Skill Name
description: One sentence description
tags: [category, topic, use-case]
---
```

**Commands**:
```yaml
---
description: What this command does (one sentence)
---
```

---

## Resources

### Complete Plugin Template

```
new-plugin/
├── .claude-plugin/
│   └── plugin.json
├── agents/
│   └── domain-expert.md
├── skills/
│   ├── domain-knowledge.md
│   └── methodology.md
└── commands/
    ├── quick-action.md
    └── detailed-action.md
```

### plugin.json Template

```json
{
  "name": "new-plugin",
  "description": "Clear 5-10 word description of plugin purpose",
  "version": "1.0.0",
  "author": {
    "name": "Personal Team"
  },
  "tags": [
    "domain-tag",
    "function-tag",
    "personal"
  ]
}
```

### Agent File Template

```markdown
---
description: Expert in [domain] for [purpose]
---

# [Agent Name] Agent

You are a **[role description]** for Personal.

Your expertise: [specific domain knowledge and approach]

## Your Approach
1. [Step 1]
2. [Step 2]
...

## Skills Available
- `skill-name-1` - Use when [condition]
- `skill-name-2` - Use when [condition]
```

### Skill File Template

```markdown
---
title: Skill Name
description: One sentence description
tags: [category, topic]
---

# Skill Name

## Metadata
**Purpose**: What this provides
**Applies to**: When to use this
**Version**: X.Y.Z

---

## Instructions
[Core knowledge, always loaded when activated]

---

## Resources
[Detailed examples, loaded on explicit request]
```

### Command File Template

```markdown
---
description: What this command does
---

# Command Name

You are a [role] performing [task].

## Command Parameters
[Reference `marketplace-command-patterns` skill for standard parameters]

## Objective
[What this command accomplishes]

## Process
1. [Step 1]
2. Activate skill: `skill-name`
3. [Step 3]

## Output Format
[How to structure the output]
```
