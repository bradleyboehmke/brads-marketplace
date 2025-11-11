# 🤖 Agents

Agents are AI personas with specialized domain expertise. Each agent has a defined role, expertise areas, and access to specific skills. When a command is invoked, it activates an agent who uses their skills to perform the task.

## What Are Agents?

Agents are **domain expert personas** that provide:
- **Consistent reasoning** across multiple commands
- **Specialized expertise** in their domain
- **Access to relevant skills** for their tasks
- **Interactive workflows** with the user

## How Agents Work

1. **Activation** - Command invokes agent (e.g., `/git-workflow:draft-commit` activates `git-workflow-specialist`)
2. **Skill Loading** - Agent loads required skills (e.g., `commit-message-standards`)
3. **Analysis** - Agent analyzes context using skill knowledge
4. **Execution** - Agent performs task and returns results to command
5. **Output** - Command formats agent's work for user

## Agent Progressive Disclosure

Agents use **progressive disclosure** to minimize token usage:
- **Agent metadata** loaded first (~100 tokens)
- **Skills loaded on demand** (metadata → instructions → resources)
- **Only required knowledge** activated for each task

This approach saves ~40% tokens compared to loading all knowledge upfront.

## Available Agents

### git-workflow-specialist

**Domain:** Git and GitHub collaboration workflows

**Expertise:**
- Git best practices (branching, staging, committing)
- Commit message standards (Conventional Commits)
- GitHub workflows (PR creation, issue management)
- Code review and quality checks

**Skills Available:**
- `commit-message-standards` - Conventional Commits format and quality
- `pr-quality-standards` - Pull request best practices
- `github-workflow-patterns` - Branch naming, issue linking, workflows

**Used By Commands:**
- All git-workflow commands

**Characteristics:**
- Standards-focused and detail-oriented
- Interactive and seeks user approval
- Provides actionable guidance
- Respects existing project conventions

---

### readme-author

**Domain:** README documentation creation and maintenance

**Expertise:**
- Project analysis and structure understanding
- README best practices and completeness
- Technical writing for developer audiences
- Framework and dependency documentation

**Skills Available:**
- `readme-standards` - README structure and content requirements
- `readme-authoring` - Writing techniques and patterns

**Used By Commands:**
- `/document-generator:generate-readme`
- `/document-generator:update-readme`
- `/document-generator:validate-readme`

**Characteristics:**
- Thorough project analysis
- Clear, concise technical writing
- Follows industry best practices
- Adapts to project type and framework

---

### adr-author

**Domain:** Architecture Decision Records (ADRs)

**Expertise:**
- MADR (Markdown Any Decision Records) format
- Architectural decision documentation
- Technical decision-making frameworks
- Consequence analysis

**Skills Available:**
- `adr-authoring` - MADR format and decision documentation

**Used By Commands:**
- `/document-generator:generate-adr`

**Characteristics:**
- Structured interview approach
- Focuses on context and consequences
- Ensures completeness
- MADR format compliance

---

### mermaid-expert

**Domain:** Architecture visualization with Mermaid diagrams

**Expertise:**
- Mermaid diagram syntax (all types)
- Architecture visualization patterns
- System flow and component diagrams
- C4, sequence, flowchart, ER diagrams

**Skills Available:**
- `mermaid-diagramming` - Comprehensive Mermaid syntax and patterns

**Used By Commands:**
- `/document-generator:generate-architecture-diagram`

**Characteristics:**
- Visual thinking and abstraction
- Multiple diagram type expertise
- Code analysis for architecture
- Clear, readable diagrams

---

### plugin-architect

**Domain:** Marketplace plugin design and architecture

**Expertise:**
- Plugin architecture principles
- Agent/skill/command patterns
- Progressive disclosure design
- Token optimization
- Skill reusability

**Skills Available:**
- `plugin-architecture-principles` - Core design patterns
- `plugin-design-template` - Standard plugin structure
- `plugin-structure-standards` - File organization and naming
- `marketplace-command-patterns` - Command design patterns
- `content-optimization-patterns` - Token optimization techniques
- `marketplace-registration` - Plugin registration and metadata
- `progressive-disclosure` - Three-tier knowledge loading

**Used By Commands:**
- All marketplace-dev commands

**Characteristics:**
- Architecture-first thinking
- Token budget awareness
- Reusability-focused
- Standards compliance
- Comprehensive planning

---

### documentation-assistant

**Domain:** Structured note-taking from work sessions

**Expertise:**
- Conversation analysis
- Template-based content generation
- Git commit interpretation
- Interactive content proposal

**Skills Available:**
- `content-generation` - Strategies for generating note content
- `organization-config` - Template and directory configuration

**Used By Commands:**
- `/note-taker:document-work`

**Characteristics:**
- Context-aware analysis
- Template-driven approach
- Interactive field-by-field workflow
- Leverages conversation history

---

### course-architect

**Domain:** Educational content creation for data science courses

**Expertise:**
- Pedagogical design for technical content
- Data science and ML curriculum
- Code example creation
- Assessment development
- Jupyter notebook authoring

**Skills Available:**
- `pedagogy` - Teaching principles for technical content
- `content-templates` - Templates for various content types
- `courses/*` - Course-specific profiles and standards

**Used By Commands:**
- All course-builder commands

**Characteristics:**
- Pedagogically sound design
- Technical accuracy focus
- Clear code examples
- Progressive difficulty
- Student-centered approach

---

## Agent Interaction Patterns

### Interview Pattern

Used by: `adr-author`, `plugin-architect`, `course-architect`

**Characteristics:**
1. Series of focused questions
2. Gathers comprehensive context
3. Validates understanding
4. Generates structured output

### Analysis Pattern

Used by: `git-workflow-specialist`, `readme-author`, `mermaid-expert`

**Characteristics:**
1. Analyzes project/codebase context
2. Applies domain knowledge
3. Generates proposals
4. Interactive approval

### Guided Workflow Pattern

Used by: `documentation-assistant`, `git-workflow-specialist`

**Characteristics:**
1. Step-by-step process
2. Interactive decisions at each step
3. Context builds throughout workflow
4. Final output after all steps

## Agent Best Practices

### For Users

- **Trust the agent's expertise** - They follow industry standards
- **Provide context when asked** - Better input → better output
- **Review proposals carefully** - You have final approval
- **Edit as needed** - Agents provide starting points, not final answers

### For Developers

- **Single responsibility** - Each agent has one clear domain
- **Skill composition** - Agents reuse skills across plugins
- **Progressive loading** - Load metadata first, details on demand
- **Interactive workflows** - Seek approval for significant actions

## Next Steps

- See [Skills](./skills.md) for knowledge modules agents use
- See [Commands](./commands.md) for how to invoke agents
- See [Architecture](../architecture.md) for agent design patterns
