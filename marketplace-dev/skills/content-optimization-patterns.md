---
title: Content Optimization Patterns
description: Strategies for reducing verbosity and improving token efficiency in plugin content
tags: [optimization, verbosity, efficiency, token-usage]
---

# Content Optimization Patterns

## Metadata

**Purpose**: Guide content optimization for token efficiency without sacrificing clarity
**Applies to**: All plugin components (agents, skills, commands)
**Version**: 1.0.0

---

## Instructions

### Core Optimization Principles

**Balance**: Optimize for clarity AND conciseness, not just brevity
**Context**: Consider the audience - developers need enough information to act
**Impact**: Focus on high-impact reductions (not micro-optimizations)

### Common Verbosity Patterns

#### 1. Redundant Section Headers

**Verbose**:
```markdown
## What This Command Does

This command validates your documentation against standards.

## Purpose

The purpose of this command is to validate documentation.
```

**Optimized**:
```markdown
## Objective

Validate documentation against standards.
```

**Savings**: ~30 tokens
**Risk**: Low - merged sections maintain clarity

#### 2. Repetitive Phrasing

**Verbose**:
```markdown
- This skill provides guidance on...
- This skill helps you understand...
- This skill contains information about...
```

**Optimized**:
```markdown
- Guidance on...
- Understanding...
- Information about...
```

**Savings**: 10-15 tokens per bullet
**Risk**: Low - context is clear from structure

#### 3. Over-Explained Examples

**Verbose**:
```markdown
**Example**:
For instance, if you wanted to validate documentation, you would run the following command. This command will analyze your project and output results:
\```bash
/validate-docs
\```
```

**Optimized**:
```markdown
**Example**:
\```bash
/validate-docs
\```
```

**Savings**: ~25 tokens
**Risk**: Low if example is self-explanatory

#### 4. Verbose Instructions

**Verbose**:
```markdown
You should first read the documentation file, and then after reading it, you need to analyze the contents of that file, and subsequently you must compare it against the standards that have been defined.
```

**Optimized**:
```markdown
1. Read documentation file
2. Analyze contents
3. Compare against standards
```

**Savings**: ~15-20 tokens
**Risk**: Low - lists are clearer than run-on sentences

#### 5. Redundant "Important" Markers

**Verbose**:
```markdown
**IMPORTANT**: This is important to note.
**NOTE**: Please note the following.
**WARNING**: Be warned about this.
```

**Optimized**:
```markdown
**Important**: [statement]
**Note**: [statement]
**Warning**: [statement]
```

OR remove if not truly critical:
```markdown
[statement]
```

**Savings**: 5-10 tokens per marker
**Risk**: Medium - ensure truly important items remain marked

#### 6. Example Bloat

**Verbose**: 10 examples of the same pattern

**Optimized**: 2-3 representative examples, reference pattern

**Savings**: 50-100+ tokens
**Risk**: Low if examples are truly redundant

#### 7. Meta-Commentary

**Verbose**:
```markdown
Now that we have discussed the above concepts, let's move on to the next section where we will explore...
```

**Optimized**:
```markdown
## Next Topic
```

**Savings**: ~15 tokens per transition
**Risk**: Low - headings provide structure

### Emoji Usage Guidelines

**When to AVOID emojis** (marketplace standard):
- Commands: ❌ Professional, concise instructions
- Skills: ❌ Reference materials for developers
- Agents: ❌ Expert personas, not casual chatbots
- Error messages: ❌ Clarity over decoration

**When emojis are acceptable**:
- User-facing output (if explicitly requested)
- Documentation examples (sparingly)
- Celebratory messages (completion confirmations)

**Token cost**: 1-3 tokens per emoji
**Clarity cost**: Can obscure meaning for screen readers, international audiences

### Redundancy Detection Patterns

#### Cross-Component Redundancy

**Pattern**: Same content in multiple files

**Detection**:
1. Compare similar sections across files
2. Look for copy-pasted paragraphs
3. Check for duplicated templates/examples

**Fix**:
- Extract to shared skill
- Reference skill from multiple components
- Use skill activation instead of inline content

**Example**:
```markdown
# Before (in 3 command files)
## Output Parameters
- --format=console (default)
- --format=markdown
...detailed explanation...

# After
## Output Parameters
Activate skill: `marketplace-command-patterns` for standard parameter details.
```

#### Internal Redundancy

**Pattern**: Same information repeated within a file

**Detection**:
1. Search for repeated phrases
2. Look for similar examples
3. Check for restated concepts

**Fix**:
- Consolidate duplicate sections
- Remove redundant examples
- Use cross-references instead of repetition

### Conciseness Optimization Strategies

#### 1. Active Voice Over Passive

**Verbose**: "The file should be read by the agent"
**Optimized**: "Agent reads the file"
**Savings**: ~2-3 tokens per sentence

#### 2. Direct Instructions Over Explanatory

**Verbose**: "You will need to make sure that you..."
**Optimized**: "Ensure you..."
**Savings**: ~3-5 tokens per instruction

#### 3. Lists Over Prose

**Verbose**: Paragraph explaining 5 steps
**Optimized**: Numbered list with 5 items
**Savings**: 10-20 tokens
**Clarity**: Improved

#### 4. Tables Over Repeated Structure

**Verbose**: 5 paragraphs with "X does Y, Z is W" pattern
**Optimized**: Table with X, Y, Z, W columns
**Savings**: 15-30 tokens
**Clarity**: Improved

#### 5. Code Over Explanation

**Verbose**: "The JSON file should have a name field, and a description field, and a version field..."
**Optimized**:
```json
{
  "name": "...",
  "description": "...",
  "version": "..."
}
```
**Savings**: 10-15 tokens

### Optimization Decision Framework

Use this framework to decide if optimization is worth it:

```
Is content redundant or verbose?
│
├─ Redundant (duplicated elsewhere)?
│  ├─ YES → Extract to skill, reference instead (HIGH PRIORITY)
│  └─ NO → Continue
│
├─ Verbose (can be shortened without losing meaning)?
│  ├─ YES, significant savings (20+ tokens)
│  │  └─ Does it reduce clarity?
│  │     ├─ NO → Optimize (MEDIUM PRIORITY)
│  │     └─ YES → Keep verbose version (clarity wins)
│  └─ NO → Keep as-is
│
└─ Micro-optimization (< 10 token savings)?
   └─ Skip (not worth the effort)
```

### Quality Gates

Before optimizing content, ensure:
- [ ] Meaning is preserved
- [ ] Examples remain clear
- [ ] Instructions are still actionable
- [ ] Technical accuracy maintained
- [ ] No critical context lost

---

## Resources

### Optimization Checklist

When reviewing content for optimization:

**Redundancy Checks**:
- [ ] Search for duplicate paragraphs across files
- [ ] Check for repeated examples
- [ ] Look for similar explanations in multiple places
- [ ] Identify extractable patterns

**Verbosity Checks**:
- [ ] Count section headers (can any be merged?)
- [ ] Review transition phrases (are they necessary?)
- [ ] Examine examples (are all needed?)
- [ ] Check for passive voice
- [ ] Look for "filler" words (that, very, really, just)

**Structure Checks**:
- [ ] Can prose become lists?
- [ ] Can repeated patterns become tables?
- [ ] Can explanations become code examples?
- [ ] Are headings descriptive enough to replace intro text?

**Clarity Checks**:
- [ ] Is technical terminology necessary?
- [ ] Are instructions actionable?
- [ ] Do examples illustrate the point?
- [ ] Is the flow logical?

### Optimization Examples by Component Type

**Agent Optimization**:
```markdown
# Before (verbose)
You are an expert in the field of documentation validation. Your role is to carefully examine documentation files and assess them against predefined standards. You should take a methodical approach to this task.

# After (optimized)
You are a documentation validation expert. Assess documentation files against predefined standards using a methodical approach.
```

**Skill Optimization**:
```markdown
# Before (redundant)
## Required Fields
- name: The name of the plugin
- version: The version of the plugin
- description: The description of the plugin

## Plugin Metadata
- name field contains the plugin name
- version field contains the plugin version
- description field contains the plugin description

# After (consolidated)
## Required Fields
- name: Plugin name
- version: Plugin version
- description: Plugin description
```

**Command Optimization**:
```markdown
# Before (verbose)
## What This Command Does

This command will perform a comprehensive validation of your project's documentation against the Personal standards. It will check multiple aspects including README completeness, architecture diagrams, and ADRs.

## Objective

The objective of this command is to validate documentation.

# After (optimized)
## Objective

Validate project documentation against standards (README, architecture diagrams, ADRs).
```

### Token Impact Estimation

**Small optimization** (10-20 tokens):
- Remove redundant headers
- Consolidate similar sections
- Shorten transition phrases

**Medium optimization** (20-50 tokens):
- Extract duplicated content to skills
- Convert prose to lists/tables
- Remove unnecessary examples

**Large optimization** (50-100+ tokens):
- Eliminate cross-file redundancy
- Restructure verbose sections
- Remove entire duplicate components

### Optimization Tradeoff Considerations

When evaluating whether to optimize, consider:

**Benefits to assess**:
- Token reduction (quantify: how many tokens saved?)
- Cost savings (for frequently-used components)
- Clarity improvement (does brevity improve focus?)
- Maintenance efficiency (less to keep in sync)

**Risks to assess**:
- Context loss (is removed content genuinely redundant?)
- Clarity reduction (does brevity create ambiguity?)
- User expertise required (does optimization assume more knowledge?)
- Refactoring effort (is the change worth the time?)

**Decision criteria**:

Optimize aggressively when:
- Skills loaded frequently
- Commands with >500 lines
- Content with clear redundancy
- Production-ready plugins

Be conservative when:
- Complex technical concepts
- New user onboarding content
- Safety-critical instructions
- Prototype/experimental plugins
