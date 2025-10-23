# Architecture

## Introduction

Brad's Marketplace follows a modular, single-purpose plugin architecture designed for Claude Code. The architecture prioritizes minimal token usage, maximum composability, and progressive disclosure of information.

This design philosophy ensures that plugins remain lightweight, focused, and efficient while providing powerful functionality through composition.

## Design Principles

### 1. Single Responsibility
Each plugin solves one specific problem well. Plugins typically contain 3-4 components on average, ensuring they remain focused and maintainable.

**Benefits:**
- Easier to understand and maintain
- Clear purpose and scope
- Reduced complexity
- Better testability

### 2. Minimal Token Usage
The architecture minimizes context window consumption through progressive disclosure:
- **Metadata first:** Plugin name and description loaded initially
- **Instructions on activation:** Full prompts loaded when command/agent is invoked
- **Resources on demand:** Skills and supporting files loaded only when needed

**Benefits:**
- Faster load times
- Reduced memory footprint
- More efficient context usage
- Better performance at scale

### 3. Composability
Plugins are designed to work independently and can be combined without conflicts. Each plugin is self-contained with clear interfaces.

**Benefits:**
- Mix and match plugins as needed
- No hidden dependencies
- Predictable behavior
- Easy to extend

### 4. Progressive Disclosure
Information is revealed incrementally based on need:
1. Plugin list shows names and descriptions
2. Command invocation loads full instructions
3. Agent activation loads expertise and skills
4. Skills loaded only when agent needs them

**Benefits:**
- Optimal context window usage
- Faster initial load
- Scales to many plugins
- Pay-for-what-you-use model

## Plugin Patterns

The marketplace supports four primary design patterns, each suited to different complexity levels:

### Pattern 1: Single-Purpose Command
**Best for:** Simple, focused tools that perform one specific action

**Structure:**
```
plugin-name/
└── commands/
    └── action-name.md
```

**When to use:**
- Single, well-defined task
- No domain expertise required
- Minimal context needed
- Quick execution

**Example:** A command that formats code snippets or converts file formats

### Pattern 2: Agent + Commands
**Best for:** Tasks requiring domain expertise with automation

**Structure:**
```
plugin-name/
├── agents/
│   └── expert-name.md
└── commands/
    ├── action-1.md
    └── action-2.md
```

**When to use:**
- Requires specialized knowledge
- Benefits from AI expertise
- Multiple related tasks
- Guidance and automation needed

**Example:** Code review plugin with review agent and specific command workflows

### Pattern 3: Full Plugin with Skills
**Best for:** Complex domains with substantial knowledge bases

**Structure:**
```
plugin-name/
├── agents/
│   └── expert-name.md
├── commands/
│   ├── action-1.md
│   └── action-2.md
└── skills/
    ├── knowledge-area-1/
    └── knowledge-area-2/
```

**When to use:**
- Complex domain requiring deep knowledge
- Large reference materials needed
- Agent needs specialized expertise
- Progressive loading of knowledge important

**Example:** Architecture validation plugin with standards, patterns, and best practices

### Pattern 4: Workflow Orchestration
**Best for:** Multi-step processes with decision points

**Structure:**
```
plugin-name/
└── commands/
    ├── orchestrate-workflow.md
    ├── step-1.md
    └── step-2.md
```

**When to use:**
- Sequential multi-step processes
- User interaction needed between steps
- Conditional branching required
- State management across steps

**Example:** Documentation plugin that analyzes work, selects templates, and creates notes

## Component Types

### Commands
Slash commands that users can invoke directly from the Claude Code interface.

**Location:** `plugins/{plugin-name}/commands/{command-name}.md`

**Purpose:**
- Execute specific actions or workflows
- Provide interactive user experiences
- Orchestrate multi-step processes

**Characteristics:**
- Self-contained instructions
- Clear user-facing functionality
- Can invoke agents or work standalone
- Loaded only when invoked

**Example:**
```markdown
# document-work

Help the user document their project work by creating structured notes.

## Instructions
1. Analyze git commits from today
2. Review conversation history
3. Guide user through template selection
...
```

### Agents
AI personas with specialized expertise and knowledge.

**Location:** `plugins/{plugin-name}/agents/{agent-name}.md`

**Purpose:**
- Provide domain-specific expertise
- Guide users through complex tasks
- Apply specialized knowledge
- Can access skills for deeper knowledge

**Characteristics:**
- Defined expertise and personality
- Can be invoked by commands or directly
- Access to plugin skills
- Progressive loading of capabilities

**Example:**
```markdown
# plugin-architect

You are an expert plugin architect for Claude Code marketplaces.

## Expertise
- Single responsibility principle
- Context efficiency patterns
- Plugin design patterns
...
```

### Skills
Reusable knowledge modules that agents can access on demand.

**Location:** `plugins/{plugin-name}/skills/{skill-name}/`

**Purpose:**
- Provide deep domain knowledge
- Store reference materials
- Share knowledge across agents
- Enable progressive disclosure

**Characteristics:**
- Only loaded when agent needs them
- Can contain multiple files
- Organized by topic/domain
- Minimize token usage until needed

**Example:**
```
skills/
├── architecture-principles/
│   ├── single-responsibility.md
│   ├── composability.md
│   └── token-efficiency.md
└── plugin-templates/
    ├── command-template.md
    └── agent-template.md
```

## Examples from This Marketplace

### note-taker: Workflow Orchestration Pattern

The `note-taker` plugin follows the workflow orchestration pattern, guiding users through a multi-step documentation process.

**Structure:**
```
plugins/note-taker/
└── commands/
    └── document-work.md
```

**Key features:**
- Single command orchestrates entire workflow
- Analyzes git commits and conversation history
- Interactive prompts for user decisions
- Templates loaded progressively
- Generates structured notes

**Token efficiency:**
- Only loaded when `/note-taker:document-work` is invoked
- Templates read on-demand based on user selection
- Conversation context already in memory (no extra load)

### marketplace-dev: Full Plugin with Skills Pattern

The `marketplace-dev` plugin demonstrates the full pattern with agents, commands, and skills.

**Structure:**
```
plugins/marketplace-dev/
├── agents/
│   └── plugin-architect.md
├── commands/
│   ├── create-plugin.md
│   └── validate-plugin.md
└── skills/
    ├── architecture-principles/
    └── plugin-templates/
```

**Key features:**
- Agent provides expert consultation
- Commands automate plugin creation and validation
- Skills contain deep architectural knowledge
- Progressive loading of expertise

**Token efficiency:**
- Plugin metadata loaded on marketplace add
- Agent loaded only when consulted or invoked by commands
- Skills loaded only when agent needs specific knowledge
- Commands work independently or with agent

**Component breakdown:**
1. **plugin-architect agent** (200 tokens) - Core expertise
2. **create-plugin command** (150 tokens) - Creation workflow
3. **validate-plugin command** (100 tokens) - Validation logic
4. **architecture-principles skill** (500 tokens) - Loaded when needed
5. **plugin-templates skill** (300 tokens) - Loaded when needed

**Total plugin cost:**
- At rest: ~50 tokens (metadata only)
- Running command: ~150-200 tokens
- With agent: ~350-450 tokens
- With skills: Up to 1,250 tokens (but only when needed)

## Best Practices

### Choosing a Pattern

**Start simple:**
- Begin with Pattern 1 (Single Command) if possible
- Add complexity only when justified
- Most tasks fit in Pattern 1 or 2

**Add an agent when:**
- Domain expertise significantly improves outcomes
- User needs guidance through complex decisions
- Multiple related tasks benefit from shared expertise

**Add skills when:**
- Reference materials are substantial (>500 tokens)
- Knowledge is reusable across multiple operations
- Progressive loading provides clear benefit

### Keeping Plugins Focused

**Good plugin scope:**
- Solves one specific problem
- Has 3-4 components on average
- Clear, single-sentence description
- No feature creep

**Signs of scope creep:**
- Description requires multiple sentences
- More than 5-6 components
- Unrelated functionality bundled together
- "Swiss army knife" approach

**Solution:**
- Split into multiple focused plugins
- Each plugin maintains single responsibility
- Plugins can work together through composition

### Optimizing Token Usage

**Command optimization:**
- Keep instructions concise and clear
- Load resources on-demand, not upfront
- Use conversation context when available
- Avoid redundant information

**Agent optimization:**
- Define core expertise briefly
- Reference skills instead of embedding knowledge
- Load skills progressively as needed
- Keep persona focused

**Skill optimization:**
- Organize by logical topics
- One skill = one knowledge area
- Reference other skills when needed
- Use clear, scannable structure

## Conclusion

This architecture enables a scalable marketplace of focused, efficient plugins. By following these patterns and principles, plugins remain:
- **Lightweight** - Minimal token overhead
- **Focused** - Single responsibility per plugin
- **Composable** - Work independently and together
- **Efficient** - Progressive disclosure of information

The result is a marketplace that scales to many plugins without overwhelming the context window or degrading performance.

