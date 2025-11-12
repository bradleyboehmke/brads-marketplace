# 🧠 Skills

Skills are reusable knowledge modules that agents activate on demand. They package domain expertise, best practices, and standards in a token-efficient format using progressive disclosure.

## What Are Skills?

Skills are **domain knowledge packages** that provide:
- **Specialized expertise** agents can reference
- **Best practices** and standards
- **Reusable knowledge** shared across plugins
- **Progressive disclosure** to minimize token usage

## How Skills Work

Skills use a three-tier progressive disclosure structure:

### Tier 1: Metadata (~75 tokens, always loaded)
- Skill name and purpose
- When to activate
- Brief description
- Usage context

### Tier 2: Instructions (~500-1500 tokens, when activated)
- Core knowledge for execution
- Standards and patterns
- Key principles
- Common use cases

### Tier 3: Resources (~1000-3000 tokens, on demand)
- Detailed checklists
- Comprehensive examples
- Edge cases
- Reference material

**Result:** ~40% token savings while maintaining full capability when needed.

## Skill Catalog

### Git Workflow Skills

#### commit-message-standards

**Purpose:** Standard commit message format and quality expectations

**When to Use:** Drafting or validating commit messages

**Key Knowledge:**
- Conventional Commits format
- Message structure (type, scope, subject, body, footer)
- Common types (feat, fix, docs, style, refactor, test, chore)
- Scope guidelines
- Breaking change notation

**Used By:** `git-workflow-specialist` agent

---

#### pr-quality-standards

**Purpose:** Pull request quality and readiness expectations

**When to Use:** Drafting or validating pull requests

**Key Knowledge:**
- PR title formatting
- Description structure (summary, changes, test plan)
- Checklist items
- Reviewer guidance
- Best practices

**Used By:** `git-workflow-specialist` agent

---

#### github-workflow-patterns

**Purpose:** GitHub collaboration patterns and conventions

**When to Use:** Working with branches, issues, or reviews

**Key Knowledge:**
- Branch naming conventions
- Issue linking patterns
- Review workflows
- Merge strategies
- Labels and milestones

**Used By:** `git-workflow-specialist` agent

---

### Documentation Skills

#### readme-standards

**Purpose:** README structure and content requirements

**When to Use:** Creating or validating READMEs

**Key Knowledge:**
- Required sections
- Content completeness criteria
- Best practices for each section
- Framework-specific conventions
- Badge guidelines

**Used By:** `readme-author` agent

---

#### readme-authoring

**Purpose:** README writing techniques and patterns

**When to Use:** Generating README content

**Key Knowledge:**
- Technical writing principles
- Code example formatting
- Installation instructions
- Usage examples
- Troubleshooting sections

**Used By:** `readme-author` agent

---

#### changelog-standards

**Purpose:** Changelog format and versioning standards

**When to Use:** Creating or updating changelogs

**Key Knowledge:**
- Keep a Changelog format
- Semantic versioning
- Calendar versioning
- Entry categorization
- Git history integration

**Used By:** `readme-author`, `adr-author` agents

---

#### adr-authoring

**Purpose:** Architecture Decision Record creation using MADR format

**When to Use:** Documenting architectural decisions

**Key Knowledge:**
- MADR template structure
- Decision context capture
- Options analysis
- Consequence documentation
- Status tracking

**Used By:** `adr-author` agent

---

#### mermaid-diagramming

**Purpose:** Mermaid diagram syntax for all diagram types

**When to Use:** Creating architecture visualizations

**Key Knowledge:**
- Flowchart syntax
- Sequence diagrams
- C4 diagrams
- Class/ER diagrams
- State diagrams
- Gantt charts

**Used By:** `mermaid-expert` agent

---

#### git-history-analysis

**Purpose:** Git commit analysis for changelog and documentation generation

**When to Use:** Extracting version history from git

**Key Knowledge:**
- Git log parsing
- Commit categorization
- Version detection
- Date extraction
- Change summarization

**Used By:** `readme-author`, `adr-author` agents

---

#### version-validation

**Purpose:** Validation rules for semantic and calendar versioning

**When to Use:** Validating or auto-incrementing version numbers

**Key Knowledge:**
- Semantic versioning (SemVer) format
- Calendar versioning (CalVer) format
- Version increment rules
- Version comparison logic
- Date format validation

**Used By:** `readme-author`, `adr-author` agents

---

#### diagram-analysis

**Purpose:** Understanding system architecture to choose appropriate diagram types

**When to Use:** Planning architecture diagrams

**Key Knowledge:**
- System architecture patterns
- Diagram type selection
- Scope determination
- Component discovery
- Visualization planning

**Used By:** `mermaid-expert` agent

---

### Marketplace Development Skills

#### plugin-architecture-principles

**Purpose:** Core architectural principles for marketplace plugins

**When to Use:** Designing or reviewing plugins

**Key Knowledge:**
- Single responsibility principle
- Progressive disclosure
- Agent/skill/command separation
- Token optimization
- Composability patterns

**Used By:** `plugin-architect` agent

---

#### plugin-design-template

**Purpose:** Standard plugin structure and design

**When to Use:** Creating new plugins

**Key Knowledge:**
- Directory structure
- File naming conventions
- Metadata requirements
- Agent/skill templates
- Command patterns

**Used By:** `plugin-architect` agent

---

#### plugin-structure-standards

**Purpose:** File organization and naming standards

**When to Use:** Organizing plugin files

**Key Knowledge:**
- `.claude-plugin/` structure
- Agent file format
- Skill organization
- Command file format
- Naming conventions

**Used By:** `plugin-architect` agent

---

#### marketplace-command-patterns

**Purpose:** Command design patterns and best practices

**When to Use:** Designing command workflows

**Key Knowledge:**
- Command structure
- Parameter handling
- Interactive patterns
- Output formatting
- Error handling

**Used By:** `plugin-architect` agent

---

#### content-optimization-patterns

**Purpose:** Token optimization techniques

**When to Use:** Optimizing skill or agent content

**Key Knowledge:**
- Progressive disclosure implementation
- Redundancy elimination
- Concise instruction writing
- Resource tier organization
- Token budgeting

**Used By:** `plugin-architect` agent

---

#### marketplace-registration

**Purpose:** Plugin registration and marketplace metadata

**When to Use:** Publishing plugins to marketplace

**Key Knowledge:**
- `marketplace.json` format
- `plugin.json` structure
- Metadata requirements
- Versioning strategy
- Tags and categories

**Used By:** `plugin-architect` agent

---

#### progressive-disclosure

**Purpose:** Three-tier knowledge loading implementation

**When to Use:** Designing skill structure

**Key Knowledge:**
- Tier 1: Metadata design
- Tier 2: Instruction writing
- Tier 3: Resource organization
- Activation triggers
- Token budget allocation

**Used By:** `plugin-architect` agent

---

### Note-Taking Skills

#### content-generation

**Purpose:** Strategies for generating note content from context

**When to Use:** Creating notes from work sessions

**Key Knowledge:**
- Conversation analysis techniques
- Git commit interpretation
- Template field population
- Content proposal strategies

**Used By:** `documentation-assistant` agent

---

#### organization-config

**Purpose:** Template and directory configuration

**When to Use:** Setting up note-taking workflows

**Key Knowledge:**
- Template discovery
- Organization structure
- Directory mapping
- Filename generation
- Path resolution

**Used By:** `documentation-assistant` agent

---

### Course Building Skills

#### pedagogy

**Purpose:** Teaching principles for technical content

**When to Use:** Creating educational materials

**Key Knowledge:**
- Learning objectives design
- Progressive difficulty
- Code example principles
- Assessment design
- Student engagement

**Used By:** `course-architect` agent

---

#### content-templates

**Purpose:** Templates for various educational content types

**When to Use:** Scaffolding course materials

**Key Knowledge:**
- Chapter structure
- Lab assignment format
- Quiz patterns
- Slide layouts
- TA guide structure

**Used By:** `course-architect` agent

---

#### courses/*

**Purpose:** Course-specific profiles and standards

**When to Use:** Creating content for specific courses

**Key Knowledge:**
- Course-specific standards
- Topic coverage
- Code style preferences
- Assessment rubrics
- Tool configurations

**Used By:** `course-architect` agent

---

## Skill Reusability

Skills can be shared across multiple agents and plugins:

| Skill | Used By Agents | Plugins |
|-------|---------------|---------|
| `commit-message-standards` | git-workflow-specialist | git-workflow |
| `pr-quality-standards` | git-workflow-specialist | git-workflow |
| `readme-standards` | readme-author | document-generator |
| `changelog-standards` | readme-author, adr-author | document-generator |
| `mermaid-diagramming` | mermaid-expert | document-generator |
| `git-history-analysis` | readme-author, adr-author | document-generator |
| `version-validation` | readme-author, adr-author | document-generator |
| `diagram-analysis` | mermaid-expert | document-generator |
| `plugin-architecture-principles` | plugin-architect | marketplace-dev |
| `progressive-disclosure` | plugin-architect | marketplace-dev |

## Skill Development Best Practices

### Structure
- Clear tier boundaries (metadata vs instructions vs resources)
- Frontmatter with activation triggers
- Concise, scannable format
- Examples over lengthy explanations

### Content
- Focus on "what to do" not "what it is"
- Actionable instructions
- Concrete examples
- Checklists for complex processes

### Optimization
- Eliminate redundancy
- Progressive detail levels
- Load only what's needed
- Budget tokens per tier

### Reusability
- Domain-focused, not task-specific
- Shareable across agents
- Generic enough for multiple uses
- Specific enough to be actionable

## Next Steps

- See [Agents](./agents.md) for how agents use skills
- See [Architecture](../architecture.md) for progressive disclosure details
- See [Commands](./commands.md) for workflows that activate skills
