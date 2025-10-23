---
description: Validate plugin architecture and compliance with marketplace principles
---

You are helping the user validate a Claude Code plugin to ensure it follows marketplace architecture principles.

## Your Task

Analyze an existing plugin and provide a comprehensive validation report with specific recommendations for improvement.

## Step-by-Step Process

### Step 1: Identify the Plugin

Ask the user which plugin they want to validate:
- Plugin name?
- Location (if not in this marketplace)?

Wait for their response.

### Step 2: Analyze Plugin Structure

Use the Bash and Read tools to examine the plugin structure:

1. **Check Directory Structure:**
   ```bash
   ls -la /Users/b294776/Desktop/Projects/brads-marketplace/plugins/{plugin-name}
   ```

2. **Identify Components:**
   - Does it have `agents/` directory?
   - Does it have `commands/` directory?
   - Does it have `skills/` directory?
   - Count the total number of components

3. **Read All Component Files:**
   - Use Read tool to examine each agent file
   - Use Read tool to examine each command file
   - Use Read tool to examine any skill files

### Step 3: Architecture Validation

Evaluate against core principles:

#### 1. Single Responsibility Principle

**Check:**
- [ ] Plugin has ONE clear purpose
- [ ] Purpose is evident from name and description
- [ ] No feature bloat or scope creep
- [ ] Components all serve the same domain

**Questions to Ask:**
- Can you describe the plugin's purpose in one sentence?
- Do all components support this single purpose?
- Could any component be split into a separate plugin?

**Report:**
- ✅ PASS: Clear single purpose
- ⚠️  WARN: Purpose is broad but acceptable
- ❌ FAIL: Multiple unrelated purposes (recommend split)

#### 2. Component Count (Token Efficiency)

**Check:**
- [ ] Average component count: 3-4 components
- [ ] Total components (agents + commands + skills)
- [ ] Not bloated (> 8 components is a red flag)
- [ ] Not too minimal (0 commands is invalid)

**Report:**
- ✅ PASS: {count} components (optimal range)
- ⚠️  WARN: {count} components (acceptable but on edge)
- ❌ FAIL: {count} components (too many, consider splitting)

#### 3. Composability

**Check:**
- [ ] Can work independently
- [ ] No forced dependencies on other plugins
- [ ] Clear boundaries
- [ ] Can be combined with other plugins

**Questions to Ask:**
- Can this plugin be used alone?
- Does it require other plugins to function?
- Are there any hidden dependencies?

**Report:**
- ✅ PASS: Fully composable and independent
- ⚠️  WARN: Some optional dependencies (document them)
- ❌ FAIL: Tightly coupled to other plugins

#### 4. Context Efficiency

**Check:**
- [ ] No unnecessary verbose content
- [ ] Progressive disclosure used (skills loaded on demand)
- [ ] Focused prompts without bloat
- [ ] Appropriate model selection (haiku vs sonnet)

**Report:**
- ✅ PASS: Optimized for minimal token usage
- ⚠️  WARN: Some verbosity but acceptable
- ❌ FAIL: Excessive content, needs optimization

### Step 4: Component Quality Validation

For each component type, validate:

#### Agent Files

For each agent in `agents/`:

**Check:**
1. **Frontmatter:**
   - [ ] Has `description` field
   - [ ] Description is 5-10 words
   - [ ] Description is clear and specific

2. **Structure:**
   - [ ] Clear expertise definition
   - [ ] Specific approach/methodology
   - [ ] Focused domain scope
   - [ ] Appropriate tone guidance

3. **Content Quality:**
   - [ ] Not overly verbose
   - [ ] Specific capabilities listed
   - [ ] Clear instructions
   - [ ] Examples provided (if applicable)

**Report Template:**
```
Agent: {agent-name}
- Frontmatter: ✅/⚠️/❌
- Structure: ✅/⚠️/❌
- Content: ✅/⚠️/❌
- Recommendations:
  - [Specific improvement 1]
  - [Specific improvement 2]
```

#### Command Files

For each command in `commands/`:

**Check:**
1. **Frontmatter:**
   - [ ] Has `description` field
   - [ ] Description is 5-10 words
   - [ ] Description clearly states purpose

2. **Structure:**
   - [ ] Clear task definition
   - [ ] Step-by-step process
   - [ ] Important notes section
   - [ ] Proper workflow structure

3. **Content Quality:**
   - [ ] Single, focused purpose
   - [ ] Clear, actionable steps
   - [ ] Handles edge cases
   - [ ] User interaction guidance (if applicable)

**Report Template:**
```
Command: {command-name}
- Frontmatter: ✅/⚠️/❌
- Structure: ✅/⚠️/❌
- Content: ✅/⚠️/❌
- Recommendations:
  - [Specific improvement 1]
  - [Specific improvement 2]
```

#### Skill Directories

For each skill in `skills/`:

**Check:**
1. **Structure:**
   - [ ] Properly organized
   - [ ] Clear purpose
   - [ ] Modular and reusable

2. **Documentation:**
   - [ ] Purpose documented
   - [ ] Usage explained
   - [ ] Examples provided

**Report Template:**
```
Skill: {skill-name}
- Structure: ✅/⚠️/❌
- Documentation: ✅/⚠️/❌
- Recommendations:
  - [Specific improvement 1]
```

### Step 5: Naming Conventions

**Check:**
- [ ] Plugin name is lowercase-hyphenated
- [ ] Plugin name is descriptive
- [ ] Agent names are clear (e.g., "security-expert")
- [ ] Command names are action-oriented (e.g., "scan-code")
- [ ] No abbreviations or unclear acronyms

**Report:**
- ✅ PASS: All naming follows conventions
- ⚠️  WARN: Some names could be clearer
- ❌ FAIL: Naming needs improvement

### Step 6: Documentation Validation

**Check:**
1. **Marketplace Configuration:**
   - [ ] Plugin listed in `.claude-plugin/marketplace.json`
   - [ ] Source path is correct
   - [ ] Description matches plugin

2. **Plugin Documentation:**
   - [ ] Plugin documented in `docs/plugins.md`
   - [ ] Usage examples provided
   - [ ] Commands listed
   - [ ] Installation instructions clear

**Report:**
- ✅ PASS: Fully documented
- ⚠️  WARN: Documentation incomplete
- ❌ FAIL: Missing critical documentation

### Step 7: Generate Validation Report

Create a comprehensive report with this structure:

```markdown
# Plugin Validation Report: {plugin-name}

## Executive Summary

Overall Score: {X}/10
Status: ✅ Production Ready | ⚠️ Needs Improvements | ❌ Requires Major Changes

## Architecture Analysis

### Single Responsibility
- Status: ✅/⚠️/❌
- Purpose: {one-sentence description}
- Assessment: {detailed assessment}

### Component Count
- Total Components: {count}
- Agents: {count}
- Commands: {count}
- Skills: {count}
- Status: ✅/⚠️/❌
- Assessment: {detailed assessment}

### Composability
- Status: ✅/⚠️/❌
- Dependencies: {list any dependencies}
- Assessment: {detailed assessment}

### Context Efficiency
- Status: ✅/⚠️/❌
- Assessment: {detailed assessment}

## Component Quality

### Agents
{list each agent with status and recommendations}

### Commands
{list each command with status and recommendations}

### Skills
{list each skill with status and recommendations}

## Naming Conventions
- Status: ✅/⚠️/❌
- Issues: {list any naming issues}

## Documentation
- Status: ✅/⚠️/❌
- Marketplace.json: ✅/⚠️/❌
- Plugin Docs: ✅/⚠️/❌

## Recommendations

### Critical (Must Fix)
1. {recommendation}
2. {recommendation}

### Important (Should Fix)
1. {recommendation}
2. {recommendation}

### Nice to Have
1. {recommendation}
2. {recommendation}

## Next Steps

{provide specific action items for the user}
```

### Step 8: Provide Actionable Recommendations

For each issue found, provide:

1. **What's Wrong:** Clear explanation of the problem
2. **Why It Matters:** Impact on plugin quality/usability
3. **How to Fix:** Specific, actionable steps
4. **Example:** Show before/after if applicable

### Step 9: Offer to Fix Issues

Ask the user if they would like you to:
- Fix critical issues automatically
- Help them fix important issues interactively
- Provide guidance for nice-to-have improvements

## Validation Criteria

### Excellent Plugin (9-10/10)
- ✅ Single, crystal-clear purpose
- ✅ 3-4 components (optimal)
- ✅ Fully composable
- ✅ Minimal token usage
- ✅ Perfect documentation
- ✅ All components well-structured
- ✅ Clear naming conventions

### Good Plugin (7-8/10)
- ✅ Clear purpose
- ✅ 2-6 components
- ✅ Mostly composable
- ✅ Reasonable token usage
- ⚠️ Minor documentation gaps
- ✅ Components mostly well-structured
- ⚠️ Minor naming issues

### Needs Improvement (5-6/10)
- ⚠️ Purpose somewhat clear
- ⚠️ Component count acceptable but not optimal
- ⚠️ Some composability issues
- ⚠️ Some token inefficiency
- ⚠️ Documentation incomplete
- ⚠️ Some structural issues

### Requires Major Changes (< 5/10)
- ❌ Unclear or multiple purposes
- ❌ Too many or too few components
- ❌ Not composable
- ❌ Token bloat
- ❌ Poor or missing documentation
- ❌ Structural problems

## Important Notes

- Be specific and constructive in feedback
- Explain the "why" behind each recommendation
- Prioritize critical issues over nice-to-haves
- Offer to help fix issues, don't just point them out
- Reference marketplace architecture documentation when relevant
- Be encouraging while maintaining standards

## Example Validation

```
User: Validate the note-taker plugin

Claude: I'll analyze the note-taker plugin for compliance with marketplace architecture principles.

[Runs through all validation steps]

# Plugin Validation Report: note-taker

## Executive Summary
Overall Score: 8/10
Status: ⚠️ Needs Minor Improvements

The note-taker plugin is well-structured with a clear single purpose: documenting project work using templates. It follows most architecture principles but could benefit from adding an agent for enhanced expertise.

## Architecture Analysis

### Single Responsibility
- Status: ✅
- Purpose: Automates note-taking by analyzing project work and creating structured notes
- Assessment: Crystal clear single purpose. All components serve this goal.

### Component Count
- Total Components: 1
- Commands: 1
- Status: ⚠️
- Assessment: Plugin is functional but minimal. Consider adding a documentation-expert agent to provide more value and better align with the 3-4 component average.

[... continues with full report ...]

## Recommendations

### Important (Should Fix)
1. Add a documentation-expert agent to provide expertise on writing quality notes
2. Consider adding a validate-note command to check note completeness

Would you like me to help implement these improvements?
```
