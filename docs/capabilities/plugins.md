# 🧩 Plugins

## What Are Plugins?

**Plugins** are packages that extend Claude Code with specialized capabilities for specific tasks. Each plugin in Brad's Marketplace is single-purpose and self-contained, making them easy to understand, install, and use.

Each plugin contains:
- **Agents** - Domain experts that provide reasoning and analysis
- **Skills** - Reusable knowledge modules that agents activate
- **Commands** - User-facing tools that you invoke directly

All plugins follow the **agents + skills + commands** architecture pattern for consistency and composability.

## How Plugins Work

When you install a plugin:

1. **Commands are registered** - New slash commands become available (e.g., `/git-workflow:draft-commit`)
2. **Agents are activated** - Specialized AI experts are ready to use when commands are invoked
3. **Skills are loaded** - Domain knowledge is packaged and available for agents to reference
4. **Workflows are enabled** - End-to-end processes become available (git workflow, documentation, etc.)

### Installation

Install plugins from the marketplace repository:

```bash
# Add the marketplace
claude plugin marketplace add https://github.com/bradleyboehmke/brads-marketplace

# Or from local directory
claude plugin marketplace add /path/to/brads-marketplace

# Install specific plugins
claude plugin install git-workflow@brads-marketplace
claude plugin install document-generator@brads-marketplace
claude plugin install marketplace-dev@brads-marketplace
claude plugin install note-taker@brads-marketplace
claude plugin install course-builder@brads-marketplace

# Verify installation
claude
/plugin list
```

## How to Invoke Plugins

Plugins can be invoked in three ways:

### 1. Slash Commands

Use plugin commands directly:

```bash
/git-workflow:draft-commit
/document-generator:generate-readme
/marketplace-dev:design-plugin
/note-taker:document-work
/course-builder:write-chapter
```

### 2. Natural Language Prompts

Claude recognizes task-related prompts and may automatically invoke the appropriate plugin:

- **"Help me draft a commit message"** → `git-workflow` plugin
- **"Create a README for this project"** → `document-generator` plugin
- **"Help me design a new plugin"** → `marketplace-dev` plugin

### 3. Workflow Chains

Chain multiple commands together:

```bash
# Feature development workflow
/git-workflow:create-branch
# ... make changes ...
/git-workflow:pre-commit-check
/git-workflow:draft-commit
/git-workflow:draft-pr
```

## Available Plugins

### git-workflow

**Enforce standard Git and GitHub collaboration practices with automated workflow assistance**

**Commands:**
- `/git-workflow:create-branch` - Interactive branch creation with naming guidance
- `/git-workflow:draft-commit` - Generate commit messages and handle staging
- `/git-workflow:draft-pr` - Generate PR title and description from changes
- `/git-workflow:pre-commit-check` - Run comprehensive pre-commit validation
- `/git-workflow:spec-issue` - Create implementation specs from GitHub issues
- `/git-workflow:validate-commit` - Validate commit message quality
- `/git-workflow:validate-pr` - Validate PR readiness

**Key Features:**
- Conventional Commits compliance
- Automatic file staging and detection
- Interactive workflows with user approval
- GitHub issue integration
- PR quality validation

### document-generator

**Create and maintain project documentation following best practices**

**Commands:**
- `/document-generator:generate-readme` - Create README from scratch
- `/document-generator:update-readme` - Update existing README
- `/document-generator:validate-readme` - Validate README standards
- `/document-generator:generate-changelog` - Create new CHANGELOG.md
- `/document-generator:update-changelog` - Update changelog with new entries
- `/document-generator:validate-changelog` - Validate changelog format
- `/document-generator:generate-adr` - Create Architecture Decision Records (MADR format)
- `/document-generator:generate-architecture-diagram` - Create Mermaid diagrams

**Key Features:**
- Keep a Changelog format compliance
- MADR (Markdown Any Decision Records) for ADRs
- Semantic and calendar versioning support
- Mermaid diagram generation
- Git history integration

### marketplace-dev

**Tools and expertise for building plugins that align with marketplace architecture**

**Commands:**
- `/marketplace-dev:design-plugin` - Design new plugin architecture
- `/marketplace-dev:review-plugin` - Review plugin for compliance and quality
- `/marketplace-dev:update-plugin-docs` - Verify and update marketplace docs

**Key Features:**
- Plugin architecture consultation
- Component redundancy detection
- Token budget estimation
- Progressive disclosure guidance
- Reusable skill identification

### note-taker

**Automates note-taking by analyzing project work and creating structured notes**

**Commands:**
- `/note-taker:document-work` - Create structured note from work session

**Key Features:**
- Analyzes conversation history and git commits
- Template-based note structure
- Interactive field-by-field content proposal
- Automatic filename generation with timestamps
- Multiple organization/context support

### course-builder

**Create educational content for data science, ML, AI, and MLOps courses**

**Commands:**
- `/course-builder:write-chapter` - Write textbook chapters
- `/course-builder:review-chapter` - Review chapter quality
- `/course-builder:create-companion-nb` - Create companion Jupyter notebooks
- `/course-builder:create-lab-nb` - Create lab assignment notebooks
- `/course-builder:create-quiz` - Create reading comprehension quizzes
- `/course-builder:create-slides` - Create presentation slides
- `/course-builder:create-module-overview` - Create Canvas module overviews
- `/course-builder:create-ta-guide` - Create TA guidance materials

**Key Features:**
- Course-specific profiles and standards
- Technical accuracy validation
- Code example generation
- Assessment creation
- Teaching material scaffolding

## Plugin Comparison

| Feature | git-workflow | document-generator | marketplace-dev | note-taker | course-builder |
|---------|-------------|-------------------|-----------------|------------|---------------|
| **Focus** | Git/GitHub automation | Documentation | Plugin development | Note-taking | Educational content |
| **Commands** | 7 | 8 | 3 | 1 | 8 |
| **Agents** | 1 | 3 | 1 | 1 | 1 |
| **Interactive** | ✓ | ✓ | ✓ | ✓ | ✓ |
| **File Generation** | - | ✓ | - | ✓ | ✓ |
| **Git Integration** | ✓✓ | ✓ | - | ✓ | - |
| **Standards Enforcement** | ✓✓ | ✓✓ | ✓✓ | - | ✓ |

## Next Steps

- See [Commands](./commands.md) for detailed command reference
- See [Agents](./agents.md) for agent capabilities
- See [Skills](./skills.md) for knowledge modules
- See [Usage Guide](../usage.md) for workflow examples
