# Brad's Claude Code Marketplace

Personal collection of Claude Code plugins for productivity, development workflow automation, and documentation.

## Overview

This marketplace provides AI-powered agents, skills, and commands to accelerate software development. Built on a modern plugin architecture with specialized agents and progressive knowledge disclosure, the marketplace includes tools for:

- **Development Workflow** - Git/GitHub workflow automation and standards enforcement
- **Documentation** - README, changelog, and architecture decision record generation
- **Plugin Development** - Tools for building and validating marketplace plugins
- **Note Taking** - Structured note-taking from project work
- **Course Building** - Educational content creation for data science and ML courses

## Repository Structure

```
brads-marketplace/
├── .claude-plugin/
│   └── marketplace.json          # Plugin marketplace configuration
├── course-builder/               # Educational content plugin
│   ├── agents/
│   ├── commands/
│   └── skills/
├── document-generator/           # Documentation generation plugin
│   ├── agents/
│   ├── commands/
│   └── skills/
├── git-workflow/                 # Git workflow automation plugin
│   ├── agents/
│   ├── commands/
│   └── skills/
├── marketplace-dev/              # Plugin development tools
│   ├── agents/
│   ├── commands/
│   └── skills/
├── note-taker/                   # Note-taking plugin
│   └── commands/
├── docs/                         # Comprehensive documentation
│   ├── plugins.md
│   └── usage.md
└── README.md                     # This file
```

## Available Plugins

### git-workflow

Enforce standard Git and GitHub collaboration practices with automated workflow assistance.

**Usage:** `/git-workflow:draft-commit`, `/git-workflow:draft-pr`, `/git-workflow:create-branch`, etc.

**Key Features:**
- Interactive branch creation following naming conventions
- Standards-compliant commit message generation
- PR title and description drafting from branch changes
- Pre-commit checks with project-aware validation
- Commit and PR quality validation
- GitHub issue specification planning

**Commands:**
- `create-branch` - Interactive branch creation with naming guidance
- `draft-commit` - Generate commit messages and handle staging
- `draft-pr` - Generate PR title and description from changes
- `pre-commit-check` - Run comprehensive pre-commit validation
- `spec-issue` - Create implementation specs from GitHub issues
- `validate-commit` - Validate commit message quality
- `validate-pr` - Validate PR readiness

### document-generator

Create and maintain project documentation following best practices.

**Usage:** `/document-generator:generate-readme`, `/document-generator:generate-adr`, etc.

**Key Features:**
- README generation and validation
- Changelog creation and updates (Keep a Changelog format)
- Architecture Decision Records (MADR format)
- Mermaid architecture diagrams

**Commands:**
- `generate-readme` - Create README from scratch
- `update-readme` - Update existing README
- `validate-readme` - Validate README standards
- `generate-changelog` - Create new CHANGELOG.md
- `update-changelog` - Update changelog with new entries
- `validate-changelog` - Validate changelog format
- `generate-adr` - Create Architecture Decision Records
- `generate-architecture-diagram` - Create Mermaid diagrams

### marketplace-dev

Tools and expertise for building plugins that align with marketplace architecture.

**Usage:** `/marketplace-dev:design-plugin`, `/marketplace-dev:review-plugin`, `/marketplace-dev:update-plugin-docs`

**Key Features:**
- Plugin architecture design consultation
- Component redundancy and verbosity analysis
- Documentation verification and updates
- Comprehensive architecture principles and templates

**Commands:**
- `design-plugin` - Design new plugin architecture
- `review-plugin` - Review plugin for compliance and quality
- `update-plugin-docs` - Verify and update marketplace docs

### note-taker

Creates structured notes from project work using pre-defined templates.

**Usage:** `/note-taker:document-work`

**Key Features:**
- Analyzes conversation history and git commits
- Supports multiple template types
- Interactive field-by-field content proposal
- Automatic filename generation with date stamps

### course-builder

Educational content creation for data science, ML, AI, and MLOps courses.

**Usage:** `/course-builder:write-chapter`, `/course-builder:create-lab-nb`, etc.

**Key Features:**
- Textbook chapter writing and review
- Companion Jupyter notebooks
- Lab assignments and TA guides
- Reading comprehension quizzes
- Presentation slides
- Module overviews

**Commands:**
- `write-chapter` - Write textbook chapters
- `review-chapter` - Review chapter quality
- `create-companion-nb` - Create companion notebooks
- `create-lab-nb` - Create lab assignments
- `create-quiz` - Create reading quizzes
- `create-slides` - Create presentation slides
- `create-module-overview` - Create Canvas module overviews
- `create-ta-guide` - Create TA guidance materials

## Installation

### Adding the Marketplace

To add this marketplace to your Claude Code installation:

```bash
claude plugin marketplace add https://github.com/USERNAME/brads-marketplace
```

Or from a local directory:

```bash
claude plugin marketplace add /path/to/brads-marketplace
```

### Installing Plugins

Once the marketplace is added, install specific plugins:

```bash
claude plugin install git-workflow@brads-marketplace
claude plugin install document-generator@brads-marketplace
claude plugin install marketplace-dev@brads-marketplace
claude plugin install note-taker@brads-marketplace
claude plugin install course-builder@brads-marketplace
```

View all available plugins:

```bash
claude
/plugin list
```

## Quick Start

```bash
# Navigate to any project
cd /path/to/your/project

# Create a properly-named branch
/git-workflow:create-branch

# Make your changes, then draft a commit
/git-workflow:draft-commit

# Create a pull request
/git-workflow:draft-pr

# Generate or update documentation
/document-generator:generate-readme
/document-generator:update-changelog
```

## Architecture Principles

This marketplace follows these design principles:

1. **Single Responsibility** - Each plugin does one thing well
2. **Minimal Token Usage** - Lightweight components that load only what's needed
3. **Composable** - Plugins can work independently or together
4. **Progressive Disclosure** - Load metadata first, instructions when activated, resources on demand
5. **Agent-Skill-Command Architecture** - Agents provide expertise, skills package knowledge, commands define workflows

### Three-Layer Architecture

- **Agents** - Domain expert personas (git-workflow-specialist, readme-author, plugin-architect)
- **Skills** - Reusable knowledge modules (commit standards, changelog format, architecture principles)
- **Commands** - User-facing workflows with parameters and interactive prompts

## Documentation

For detailed information:
- [Plugin Documentation](docs/plugins.md) - Detailed information about each plugin
- [Usage Guide](docs/usage.md) - Comprehensive guide on installation and usage

## Adding New Plugins

To add a new plugin:

1. Create a new directory at the root:
   ```
   your-plugin-name/
   ├── commands/        # Slash commands
   ├── agents/          # (optional) AI agents
   └── skills/          # (optional) Agent skills
   ```

2. Add to `.claude-plugin/marketplace.json`:
   ```json
   {
     "name": "your-plugin-name",
     "source": "./your-plugin-name",
     "description": "Brief description"
   }
   ```

3. Document in `docs/plugins.md`

## License

Personal use only.
