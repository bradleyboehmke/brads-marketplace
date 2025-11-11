---
title: Plugin Architecture Principles
description: Core architectural principles for Personal marketplace plugins
tags: [architecture, design-principles, best-practices]
---

# Plugin Architecture Principles

## Metadata

**Purpose**: Define core architectural principles for marketplace plugins
**Applies to**: All plugin development
**Version**: 1.0.0

---

## Instructions

### Core Philosophy

Every plugin in the Personal marketplace follows these foundational principles:

#### 1. Single Responsibility Principle
- **Each plugin does ONE thing well**
- Purpose must be describable in 5-10 words
- If description needs "and" or "or", consider splitting
- Average plugin size: 3-4 components

**Examples**:
- ✅ Good: "Validates documentation standards compliance"
- ✅ Good: "Analyzes repository architecture and risks"
- ❌ Too broad: "Validates everything and generates reports and fixes issues"

#### 2. Composability Over Bundling
- Prefer multiple focused plugins over one large plugin
- Design components to work independently
- Enable mix-and-match for custom workflows
- Avoid tight coupling between unrelated features

**Rationale**: Users can install only what they need, reducing cognitive load and token usage.

#### 3. Progressive Disclosure
- Load only what's needed when it's needed
- Three-tier skill loading:
  1. **Metadata** (always): Title, description, tags
  2. **Instructions** (when activated): Core knowledge
  3. **Resources** (on demand): Examples, reference materials
- Commands should activate skills explicitly

#### 4. Context Efficiency
- Minimize token usage at every layer
- Extract common knowledge to reusable skills
- Avoid duplication across agents/commands
- Optimize for fast, focused execution

#### 5. Clear Boundaries
- Agents provide reasoning and judgment
- Skills provide knowledge and patterns
- Commands provide orchestration and user interface
- No overlap in responsibilities

### Three-Layer Architecture

**Layer 1: Agents** (`agents/`)
- **What**: AI personas with domain expertise
- **When**: Need reasoning, judgment, or contextual decision-making
- **Size**: Typically 100-300 lines
- **Contains**: Role definition, approach, decision-making framework

**Layer 2: Skills** (`skills/`)
- **What**: Modular knowledge packages
- **When**: Reusable knowledge needed by multiple agents/commands
- **Size**: Typically 50-200 lines (instructions section)
- **Contains**: Standards, patterns, reference materials, methodologies

**Layer 3: Commands** (`commands/`)
- **What**: User-facing tools and workflows
- **When**: Invokable actions with parameters and output
- **Size**: Typically 100-400 lines (plus skill activation)
- **Contains**: Parameter handling, workflow orchestration, output formatting

### Design Decision Framework

Use this framework to decide component structure:

```
START: What problem does this plugin solve?
│
├─ Is it a single, focused problem?
│  ├─ YES → Good candidate for plugin
│  └─ NO → Consider splitting into multiple plugins
│
├─ What expertise is needed?
│  ├─ Domain reasoning → Create Agent
│  └─ Just knowledge → Use Skill
│
├─ Is the knowledge reusable?
│  ├─ YES → Create Skill
│  └─ NO → Include in Command
│
└─ How do users invoke it?
   ├─ Direct command → Create Command
   └─ Background capability → Agent + Skills only
```

### Quality Metrics

**Good Plugin Design**:
- Purpose clear in 5-10 words ✅
- 2-5 total components ✅
- No knowledge duplication ✅
- Works in isolation ✅
- Composes with others ✅

**Red Flags**:
- Purpose requires long explanation ❌
- 10+ component files ❌
- Same knowledge in multiple files ❌
- Requires other specific plugins ❌
- Duplicate functionality ❌

---

## Resources

### Anti-Patterns Reference

Watch for these common mistakes during plugin design:

**1. The Kitchen Sink**
- **Problem**: Plugin tries to do everything
- **Symptoms**: Purpose requires paragraph to explain, 10+ component files, "and/or" in description
- **Fix**: Split into multiple focused plugins
- **Example**: "Validates docs AND generates reports AND fixes code AND deploys" → Split into validator, document-generator, code-fixer, deployer plugins

**2. The Encyclopedia**
- **Problem**: Massive command files with all knowledge inline
- **Symptoms**: Commands >600 lines, same documentation repeated across commands
- **Fix**: Extract knowledge to reusable skills
- **Example**: 800-line command with inline Python standards → Extract to `python-standards` skill, reference from command

**3. The Duplicate**
- **Problem**: Same information in agent, skills, and commands
- **Symptoms**: Copy-pasted content, version drift between files, difficult updates
- **Fix**: Single source of truth in skills, reference from agents/commands
- **Example**: README template in 3 files → Create `readme-standards` skill, activate from commands

**4. The Tangle**
- **Problem**: Components with circular dependencies
- **Symptoms**: Agent A needs Agent B which needs Agent A, skills that reference each other
- **Fix**: Clear hierarchy: Commands → Agents → Skills (unidirectional flow)
- **Example**: security-agent ← → compliance-agent → Create coordinator agent that uses both

**5. The Orphan**
- **Problem**: Component that doesn't fit plugin purpose
- **Symptoms**: Component solves unrelated problem, rarely used with other components
- **Fix**: Move to separate plugin or remove
- **Example**: `format-code.md` command in a validation plugin → Move to code-formatter plugin

**6. The Monolith Skill**
- **Problem**: Single skill file with multiple unrelated domains
- **Symptoms**: Skill >400 lines, contains 3+ distinct topics, commands only use 30% of content
- **Fix**: Split into focused skills by domain
- **Example**: `all-standards.md` (docs + testing + security) → Split into 3 skills

**7. The Phantom Agent**
- **Problem**: Agent that doesn't provide reasoning, just passes knowledge through
- **Symptoms**: Agent has no decision-making logic, could be replaced with direct skill activation
- **Fix**: Remove agent, have command directly activate skills
- **Example**: Agent that only says "activate skill X" → Command activates skill X directly
