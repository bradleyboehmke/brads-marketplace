# Architecture Principles Skill

This skill provides deep knowledge of Claude Code marketplace architecture principles based on https://github.com/wshobson/agents/blob/main/docs/architecture.md.

## Purpose

Provides agents and commands with comprehensive understanding of:
- Single Responsibility Principle
- Composability patterns
- Context efficiency strategies
- Plugin design patterns
- Best practices and common pitfalls

## When to Use

Load this skill when:
- Designing new plugins
- Validating existing plugins
- Refactoring bloated plugins
- Making architectural decisions
- Teaching plugin development concepts

## Core Principles

### 1. Single Responsibility Principle

**Definition:** Each plugin does ONE thing well.

**Guidelines:**
- Plugin has a single, clear purpose describable in one sentence
- Average plugin size: 3-4 components
- All components serve the same domain/purpose
- No feature bloat or scope creep

**Good Examples:**
- `code-review`: Analyzes code quality and suggests improvements
- `api-testing`: Generates and runs API tests
- `security-scan`: Identifies security vulnerabilities

**Bad Examples:**
- `dev-tools`: Does code review, testing, deployment, and monitoring (too broad)
- `project-manager`: Handles git, tickets, docs, meetings (unrelated features)

**How to Validate:**
- Can you describe the plugin's purpose in one sentence?
- Do all components support this single purpose?
- Could any component be split into a separate plugin?

### 2. Composability

**Definition:** Plugins work independently and can be combined for complex workflows.

**Guidelines:**
- Plugin can be used standalone
- No forced dependencies on other plugins
- Clear interfaces and boundaries
- Optional integrations are documented

**Good Examples:**
- `frontend-dev` + `backend-dev` + `api-testing` = full-stack workflow
- Each works independently
- Together they cover complete development cycle

**Bad Examples:**
- `frontend-dev` requires `backend-dev` to function
- Plugin hardcodes calls to specific other plugins
- Tightly coupled components that can't be separated

**How to Validate:**
- Can this plugin be used without any other plugins?
- Are all dependencies optional and documented?
- Can it integrate with multiple other plugins?

### 3. Context Efficiency

**Definition:** Minimize token usage for faster processing and better LLM performance.

**Guidelines:**
- Load only what's needed
- Use progressive disclosure (skills loaded on demand)
- Avoid verbose or redundant content
- Choose appropriate model (haiku vs sonnet)

**Strategies:**
- **Progressive Disclosure:**
  - Tier 1: Metadata (always loaded) - name, description
  - Tier 2: Instructions (loaded when activated) - agent prompts, command steps
  - Tier 3: Resources (loaded on demand) - skills, knowledge bases

- **Content Optimization:**
  - Remove unnecessary verbose explanations
  - Use bullet points over paragraphs
  - Keep examples focused and minimal
  - Avoid repetition

- **Model Selection:**
  - Haiku: Simple, focused tasks (code formatting, linting)
  - Sonnet: Complex reasoning (architecture design, debugging)

**How to Validate:**
- Is every word necessary?
- Can skills be loaded on demand instead of upfront?
- Is the right model selected for the task?

### 4. Component Count

**Guideline:** Average 3-4 components per plugin

**Optimal Ranges:**
- 1-2 components: Acceptable for simple, focused tools
- 3-4 components: Optimal balance
- 5-6 components: Acceptable if tightly related
- 7+ components: Red flag - likely violating single responsibility

**Components Include:**
- Agents (in `agents/`)
- Commands (in `commands/`)
- Skills (in `skills/`)

**How to Validate:**
- Count total components
- If > 6, can it be split into multiple plugins?
- If = 1, would adding an agent provide more value?

## Design Patterns

### Pattern 1: Single-Purpose Command

**When to Use:**
- Simple, focused automation
- No domain expertise needed
- Quick utility or tool

**Structure:**
```
plugins/plugin-name/
└── commands/
    └── action-name.md
```

**Examples:**
- `code-formatter/commands/format-code.md`
- `lint-fixer/commands/fix-lints.md`
- `dependency-updater/commands/update-deps.md`

**Characteristics:**
- 1 component
- Fast and lightweight
- Clear input/output
- Minimal configuration

### Pattern 2: Agent + Commands

**When to Use:**
- Domain expertise enhances the tool
- Multiple related operations
- Need for contextual guidance

**Structure:**
```
plugins/plugin-name/
├── agents/
│   └── domain-expert.md
└── commands/
    ├── operation-1.md
    └── operation-2.md
```

**Examples:**
- `security-review/`
  - `agents/security-expert.md`
  - `commands/scan-vulnerabilities.md`
  - `commands/fix-security-issues.md`

**Characteristics:**
- 2-4 components
- Agent provides expertise
- Commands provide automation
- Balanced value

### Pattern 3: Full Plugin with Skills

**When to Use:**
- Complex domain requiring knowledge
- Advanced use cases
- Reusable knowledge packages

**Structure:**
```
plugins/plugin-name/
├── agents/
│   └── domain-expert.md
├── commands/
│   ├── operation-1.md
│   └── operation-2.md
└── skills/
    ├── knowledge-area-1/
    └── knowledge-area-2/
```

**Examples:**
- `kubernetes-ops/`
  - `agents/k8s-architect.md`
  - `commands/deploy-service.md`
  - `commands/scale-deployment.md`
  - `skills/helm-charts/`
  - `skills/networking/`

**Characteristics:**
- 4-6 components
- Comprehensive coverage
- Progressive disclosure
- Advanced capabilities

### Pattern 4: Workflow Orchestration

**When to Use:**
- Multi-step end-to-end process
- Coordinates multiple operations
- Complex automation

**Structure:**
```
plugins/workflow-name/
├── agents/
│   └── orchestrator.md
└── commands/
    ├── step-1.md
    ├── step-2.md
    └── step-3.md
```

**Examples:**
- `feature-development/`
  - `agents/feature-architect.md`
  - `commands/design-feature.md`
  - `commands/implement-feature.md`
  - `commands/test-feature.md`

**Characteristics:**
- 3-5 components
- Sequential workflow
- End-to-end automation
- May compose other plugins

## Common Pitfalls

### 1. Scope Creep

**Problem:** Plugin tries to do too much

**Signs:**
- More than 6-7 components
- Unrelated features bundled together
- Can't describe purpose in one sentence
- Multiple domains covered

**Solution:**
- Split into multiple focused plugins
- Remove tangential features
- Clarify core purpose

**Example:**
```
BAD: dev-toolkit (git, testing, docs, deployment, monitoring)
GOOD:
  - git-workflows (just git operations)
  - testing-automation (just testing)
  - docs-generator (just documentation)
```

### 2. Token Bloat

**Problem:** Too much content loaded unnecessarily

**Signs:**
- Verbose agent prompts
- Large example blocks always loaded
- Knowledge that could be in skills
- Repetitive content

**Solution:**
- Move knowledge to skills (load on demand)
- Reduce verbosity
- Remove redundant content
- Use progressive disclosure

### 3. Tight Coupling

**Problem:** Plugin can't work independently

**Signs:**
- Requires specific other plugins
- Hardcoded dependencies
- Can't use features separately
- Assumes specific environment

**Solution:**
- Make dependencies optional
- Document integrations
- Clear interfaces
- Standalone functionality

### 4. Poor Documentation

**Problem:** Users don't understand purpose or usage

**Signs:**
- No description or vague description
- Missing usage examples
- Unclear component purposes
- No installation instructions

**Solution:**
- Clear 5-10 word description
- Usage examples for all commands
- Document all components
- Provide installation guide

### 5. Unclear Boundaries

**Problem:** Overlaps with other plugins

**Signs:**
- Duplicate functionality
- Unclear which plugin to use
- Competing with existing plugins
- Ambiguous scope

**Solution:**
- Research existing plugins
- Define clear boundaries
- Document differences
- Consider integration instead

## Quality Checklist

Use this checklist for every plugin:

**Architecture:**
- [ ] Single, clear purpose (describable in one sentence)
- [ ] 3-4 components average (not bloated)
- [ ] Fully composable (works independently)
- [ ] Minimal token usage (optimized content)
- [ ] Clear boundaries (no overlaps)

**Components:**
- [ ] All components have frontmatter with description
- [ ] Agent prompts are focused (if applicable)
- [ ] Commands have clear step-by-step instructions
- [ ] Skills use progressive disclosure (if applicable)

**Naming:**
- [ ] Plugin name is lowercase-hyphenated
- [ ] Name is descriptive and clear
- [ ] Component names are action-oriented
- [ ] No unclear abbreviations

**Documentation:**
- [ ] Listed in marketplace.json with correct path
- [ ] Documented in docs/plugins.md
- [ ] Usage examples provided
- [ ] Installation instructions included
- [ ] Dependencies documented (if any)

## References

- [Marketplace Architecture](https://github.com/wshobson/agents/blob/main/docs/architecture.md)
- [Plugin Specification](https://github.com/wshobson/agents/blob/main/docs/plugins.md)
- [Agent Guidelines](https://github.com/wshobson/agents/blob/main/docs/agents.md)
