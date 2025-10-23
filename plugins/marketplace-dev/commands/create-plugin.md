---
description: Scaffold a new plugin following marketplace architecture principles
---

You are helping the user create a new Claude Code plugin that follows the marketplace architecture principles.

## Your Task

Guide the user through an interactive conversation to design and scaffold a new plugin with the proper structure, components, and documentation.

## Step-by-Step Process

### Step 1: Understand the Problem

Ask the user:
1. **What problem does this plugin solve?**
   - Get a clear description of the need
   - Understand the target users
   - Identify the core value proposition

2. **What's the scope?**
   - Is this a single command/tool?
   - Is this a workflow orchestrator?
   - Does it need specialized agent(s)?
   - Will it require skills/knowledge packages?

Wait for their response before proceeding.

### Step 2: Design the Plugin Architecture

Based on the problem and scope, recommend a design pattern:

**Pattern 1: Single-Purpose Command**
- For simple, focused tools
- Structure: `commands/` only
- Example: code-formatter, lint-checker

**Pattern 2: Agent + Commands**
- For domain expertise with tools
- Structure: `agents/` + `commands/`
- Example: security-review, performance-optimization

**Pattern 3: Full Plugin with Skills**
- For complex domains requiring knowledge
- Structure: `agents/` + `commands/` + `skills/`
- Example: kubernetes-ops, cloud-infrastructure

Present your recommendation and explain why. Ask the user to confirm or adjust.

### Step 3: Gather Plugin Details

Collect the following information:

1. **Plugin Name**
   - Should be lowercase, hyphenated
   - Clear and descriptive
   - Example: `security-review`, `api-testing`, `docs-generator`

2. **Plugin Description**
   - 5-10 words
   - Clear value proposition
   - Example: "Automated security analysis and vulnerability detection"

3. **Components Needed**
   - List agents (if any) with their expertise
   - List commands with their purposes
   - List skills (if any) with their content

### Step 4: Create Directory Structure

Use the Bash tool to create the plugin directory structure:

```bash
mkdir -p /Users/b294776/Desktop/Projects/brads-marketplace/plugins/{plugin-name}/{agents,commands,skills}
```

Adjust based on which components are needed (e.g., if no skills, don't create that directory).

### Step 5: Create Agent Files (if applicable)

For each agent needed:

1. Ask for agent details:
   - Agent name (e.g., "security-expert", "performance-analyzer")
   - Expertise areas (3-5 bullet points)
   - Approach/methodology

2. Use the Write tool to create the agent file at:
   `/Users/b294776/Desktop/Projects/brads-marketplace/plugins/{plugin-name}/agents/{agent-name}.md`

3. Use this template structure:

```markdown
---
description: Brief description of agent expertise (5-10 words)
---

You are a [Agent Name], an expert in [domain].

## Your Expertise

You specialize in:
- [Capability 1]
- [Capability 2]
- [Capability 3]

## Your Approach

When helping users, you:
1. [Step 1]
2. [Step 2]
3. [Step 3]

## Key Principles

- [Principle 1]
- [Principle 2]
- [Principle 3]

## [Additional sections as needed]

## Your Tone

- [Tone guidance]
```

### Step 6: Create Command Files

For each command needed:

1. Ask for command details:
   - Command name (e.g., "scan-code", "generate-tests")
   - Description (5-10 words)
   - Step-by-step workflow

2. Use the Write tool to create the command file at:
   `/Users/b294776/Desktop/Projects/brads-marketplace/plugins/{plugin-name}/commands/{command-name}.md`

3. Use this template structure:

```markdown
---
description: Brief description of what this command does (5-10 words)
---

[Opening context paragraph explaining what this command does]

## Your Task

[Clear description of the command's purpose and what it accomplishes]

## Step-by-Step Process

### Step 1: [First Step Name]

[Detailed instructions for this step]
- [Sub-step or detail]
- [Sub-step or detail]

Wait for their response before proceeding. (if interactive)

### Step 2: [Second Step Name]

[Detailed instructions for this step]
- [Sub-step or detail]
- [Sub-step or detail]

### Step 3: [Third Step Name]

[Detailed instructions for this step]

## Important Notes

- [Important consideration 1]
- [Important consideration 2]
- [Important consideration 3]
```

### Step 7: Create Skills (if applicable)

For each skill needed:

1. Ask what knowledge or resources the skill should contain
2. Create skill directory structure as needed
3. Document the skill's purpose and contents

### Step 8: Update Marketplace Configuration

Use the Edit tool to update `.claude-plugin/marketplace.json`:

```json
{
  "name": "plugin-name",
  "source": "./plugins/plugin-name",
  "description": "Brief description (5-10 words)"
}
```

Add this entry to the `plugins` array in the marketplace.json file.

### Step 9: Update Documentation

1. **Update docs/plugins.md**
   - Add new section for the plugin
   - Document all commands and agents
   - Provide usage examples
   - List any dependencies

2. **Provide Usage Example**
   - Show how to install: `/plugin install {plugin-name}`
   - Show how to use commands: `/{plugin-name}:{command-name}`
   - Include example workflow

### Step 10: Validate Plugin Design

Run through this checklist with the user:

**Architecture Validation:**
- [ ] Single, clear purpose
- [ ] 3-4 components average (not bloated)
- [ ] Minimal token usage
- [ ] Can work independently (composable)
- [ ] Clear, descriptive names

**Documentation Validation:**
- [ ] Plugin description is clear (5-10 words)
- [ ] All components have frontmatter
- [ ] Usage examples provided
- [ ] Marketplace.json updated

**Quality Validation:**
- [ ] Follows single responsibility principle
- [ ] No scope creep
- [ ] Clear boundaries
- [ ] Proper file structure

### Step 11: Provide Next Steps

Once the plugin is created, inform the user:

1. **Test the Plugin:**
   ```bash
   /plugin refresh
   /plugin install {plugin-name}
   ```

2. **Try Commands:**
   ```bash
   /{plugin-name}:{command-name}
   ```

3. **Iterate:**
   - Gather feedback
   - Refine prompts
   - Add capabilities as needed

4. **Git Workflow:**
   ```bash
   git add plugins/{plugin-name}
   git add .claude-plugin/marketplace.json
   git add docs/plugins.md
   git commit -m "Add {plugin-name} plugin"
   ```

## Important Guidelines

### Keep It Focused
- One plugin = one purpose
- If the plugin tries to do too much, suggest splitting into multiple plugins
- Average plugin should have 3-4 components

### Optimize for Tokens
- Don't include unnecessary context
- Use progressive disclosure for skills
- Keep agent prompts focused on essentials

### Ensure Composability
- Plugin should work standalone
- Should also work with other plugins
- No forced dependencies

### Document Thoroughly
- Clear descriptions
- Usage examples
- Expected inputs/outputs
- Common use cases

## Example Conversation Flow

```
Claude: Let's create a new plugin! What problem are you trying to solve?

User: I want to automate API testing

Claude: Great! Let me understand the scope:
- Will this need specialized expertise (agent) for API testing, or just commands?
- Should it generate tests, run tests, or both?
- Any specific testing frameworks or standards to follow?

User: It should have an agent that understands REST APIs and a command to generate tests

Claude: Perfect! I recommend the "Agent + Commands" pattern:
- Agent: api-testing-expert (provides REST API expertise)
- Command: generate-tests (creates test cases based on API specs)

This keeps it focused while providing both expertise and automation. Does this sound right?

User: Yes!

Claude: Let's gather some details:

1. Plugin name: "api-testing"
2. Description: "Automated API test generation and best practices"
3. Agent expertise areas - what should the expert know? (I suggest: REST principles, test coverage, edge cases)

[... continues through all steps ...]
```

## Remember

Your goal is to help users create high-quality, focused plugins that follow marketplace architecture principles. Guide them toward:

- Single-purpose designs
- Composable architectures
- Minimal token usage
- Clear documentation
- Proper structure

Be conversational, ask questions, and provide recommendations based on best practices!
