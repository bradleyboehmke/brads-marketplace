---
title: Plugin Design Document Template
description: Standard template for documenting plugin architecture and implementation plans
tags: [template, documentation, design, planning]
---

# Plugin Design Document Template

## Metadata

**Purpose**: Provide standard structure for plugin design documentation
**Applies to**: All new plugin development in marketplace
**Version**: 1.0.0

---

## Instructions

### When to Use This Template

Use this template when:
- Designing a new plugin from scratch
- Documenting architecture decisions for a plugin
- Planning refactoring of an existing plugin
- Communicating plugin design to stakeholders

### Template Sections

The design document should include these sections in order:

1. **Overview** - Purpose, use cases, scope
2. **Architecture Decision** - Pattern and rationale
3. **Component Design** - Detailed breakdown of agents, skills, commands
4. **File Structure** - Directory layout
5. **Token Budget Summary** - Estimated token usage
6. **Implementation Checklist** - Step-by-step tasks
7. **Next Steps** - Immediate actions to take

---

## Resources

### Complete Design Document Template

```markdown
# Plugin Design: [Plugin Name]

## Overview

**Purpose**: [5-10 word description]
**Use Cases**: [When users will invoke this]
**Scope**: [What's included and excluded]

## Architecture Decision

**Pattern**: [Single-purpose / Workflow orchestration / Agent + Skill integration]

**Rationale**: [Why this architecture fits the use case]

## Component Design

### Agents

#### [Agent Name] (`agents/agent-name.md`)
**Role**: [Expert persona and domain]
**Responsibilities**:
- [Responsibility 1]
- [Responsibility 2]

**Skills Used**:
- `skill-name-1` - When [condition]
- `skill-name-2` - When [condition]

**Token Budget**: ~[X] tokens

---

### Skills

#### [Skill Name] (`skills/skill-name.md`)
**Purpose**: [What knowledge this provides]
**Used By**: [Which agents/commands use this]

**Tier 1: Metadata** (~75 tokens)
- Title, description, tags

**Tier 2: Instructions** (~[X] tokens)
- [Core content outline]

**Tier 3: Resources** (~[X] tokens)
- [Detailed content outline]

**Token Budget**: ~[X] tokens (Tier 1+2 typically loaded)

---

### Commands

#### [Command Name] (`commands/command-name.md`)
**Purpose**: [What user action this enables]
**Parameters**:
- Standard output parameters (--format, --output)
- [Any custom parameters]

**Workflow**:
1. [Step 1]
2. Activate agent: `agent-name`
3. Agent activates skill: `skill-name`
4. [Processing]
5. Format output

**Token Budget**: ~[X] tokens (command) + ~[Y] tokens (agent) + ~[Z] tokens (skills)
**Total**: ~[X+Y+Z] tokens

---

## File Structure

```
plugin-name/
├── .claude-plugin/
│   └── plugin.json
├── agents/                   [if needed]
│   └── agent-name.md
├── skills/                   [if needed]
│   ├── skill-name-1.md
│   └── skill-name-2.md
└── commands/
    ├── command-1.md
    └── command-2.md
```

## Token Budget Summary

| Component | Typical Load | Max Load |
|-----------|--------------|----------|
| Agents | [X] tokens | [Y] tokens |
| Skills | [X] tokens | [Y] tokens |
| Commands | [X] tokens | [Y] tokens |
| **Total** | **[X] tokens** | **[Y] tokens** |

## Implementation Checklist

- [ ] Create plugin directory structure
- [ ] Write plugin.json
- [ ] Implement agents (if applicable)
- [ ] Implement skills with three-tier structure
- [ ] Implement commands with output parameters
- [ ] Add entry to marketplace.json
- [ ] Update root CLAUDE.md
- [ ] Test plugin installation
- [ ] Test command invocation
- [ ] Verify token usage

## Next Steps

1. **Create plugin structure**: `mkdir -p plugin-name/{.claude-plugin,agents,skills,commands}`
2. **Write plugin.json**: Define metadata and tags
3. **Implement components**: Start with commands, then agents, then skills
4. **Test iteratively**: Install and test each component as built
5. **Register in marketplace**: Add to marketplace.json when complete
```

### Token Budget Estimation Guidelines

**Agents**:
- Minimal agent (role + basic approach): ~200-300 tokens
- Standard agent (role + detailed approach + skill activation): ~400-600 tokens
- Complex agent (multiple personas + decision frameworks): ~600-800 tokens

**Skills (Instructions tier)**:
- Small skill (focused standards): ~300-500 tokens
- Medium skill (comprehensive guide): ~600-1000 tokens
- Large skill (reference material): ~1000-1500 tokens

**Commands**:
- Simple command (direct execution): ~200-400 tokens
- Standard command (parameter handling + workflow): ~400-600 tokens
- Complex command (multi-step orchestration): ~600-1000 tokens

**Total Budget Targets**:
- Simple plugin: 500-1500 tokens
- Standard plugin: 1500-3000 tokens
- Complex plugin: 3000-5000 tokens
- Avoid exceeding 5000 tokens for typical use case

### Architecture Pattern Examples

**Single-Purpose Pattern**:
```markdown
## Architecture Decision

**Pattern**: Single-Purpose Command

**Rationale**: This plugin performs one focused task (format code files). It doesn't require expert reasoning or multiple knowledge domains, so a single command without agents/skills is sufficient.

**Components**:
- 1 command: `format-code.md`
- 0 agents
- 0 skills (logic is simple enough to include in command)
```

**Agent + Skills Pattern**:
```markdown
## Architecture Decision

**Pattern**: Agent + Multiple Skills

**Rationale**: This plugin requires expert judgment (security analysis) and references multiple knowledge domains (security standards, vulnerability patterns). An agent provides the expertise, while skills contain reusable security knowledge.

**Components**:
- 1 agent: `security-auditor.md`
- 3 skills: `security-standards.md`, `vulnerability-patterns.md`, `remediation-guide.md`
- 1 command: `audit-security.md`
```

**Workflow Orchestration Pattern**:
```markdown
## Architecture Decision

**Pattern**: Workflow Orchestration

**Rationale**: This plugin coordinates a multi-step workflow (setup project, configure CI/CD, generate docs). Multiple commands handle different aspects, sharing common skills for consistency.

**Components**:
- 0 agents (no expert reasoning needed)
- 2 skills: `project-templates.md`, `configuration-standards.md`
- 4 commands: `setup-structure.md`, `configure-ci.md`, `generate-docs.md`, `full-setup.md`
```

### Design Document Best Practices

**Clarity**:
- Use concrete examples, not abstract descriptions
- Specify actual file names, not placeholders
- Provide token estimates based on actual content planned

**Completeness**:
- Address all three layers (agents, skills, commands)
- Explain rationale for architectural choices
- Include both typical and maximum token budgets

**Actionability**:
- Implementation checklist should be specific
- Next steps should be immediately actionable
- File structure should be copy-paste ready

**Realism**:
- Don't over-architect simple plugins
- Token budgets should be achievable
- Component counts should match complexity
