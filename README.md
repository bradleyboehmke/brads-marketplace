# Brad's Claude Code Marketplace

[![License](https://img.shields.io/badge/license-Personal%20Use-blue.svg)](#license)
[![Plugins](https://img.shields.io/badge/plugins-5-green.svg)](#available-plugins)
[![GitHub](https://img.shields.io/badge/github-brads--marketplace-black.svg)](https://github.com/bradleyboehmke/brads-marketplace)

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
├── .claude-plugin/        # Marketplace configuration
├── {plugin-name}/         # Each plugin directory contains:
│   ├── agents/           # Domain expert AI personas
│   ├── commands/         # User-facing slash commands
│   └── skills/           # Reusable knowledge modules
├── docs/                 # Documentation (see below)
└── README.md
```

Plugins: `git-workflow`, `document-generator`, `marketplace-dev`, `note-taker`, `course-builder`

## Available Plugins

| Plugin | Description | Key Commands |
|--------|-------------|--------------|
| **git-workflow** | Automate Git/GitHub workflows with standards enforcement | `draft-commit`, `draft-pr`, `create-branch`, `pre-commit-check` |
| **document-generator** | Generate and maintain project documentation | `generate-readme`, `generate-changelog`, `generate-adr`, `generate-architecture-diagram` |
| **marketplace-dev** | Build and validate marketplace plugins | `design-plugin`, `review-plugin`, `update-plugin-docs` |
| **note-taker** | Create structured notes from work sessions | `document-work` |
| **course-builder** | Create educational content for data science courses | `write-chapter`, `create-lab-nb`, `create-quiz`, `create-slides` |

For detailed information about each plugin, see [Plugin Documentation](docs/capabilities/plugins.md).

## Installation

### Adding the Marketplace

To add this marketplace to your Claude Code installation:

```bash
claude plugin marketplace add https://github.com/bradleyboehmke/brads-marketplace
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

## Architecture

Built on a three-layer architecture:
- **Agents** - Domain expert AI personas (e.g., git-workflow-specialist, readme-author)
- **Skills** - Reusable knowledge modules (e.g., commit standards, versioning rules)
- **Commands** - User-facing workflows (e.g., `/git-workflow:draft-commit`)

Key principles: Single responsibility, progressive disclosure, composability, minimal token usage.

For detailed architecture patterns, see [Architecture Guide](docs/architecture.md).

## Documentation

Comprehensive documentation is available in the `docs/` directory:

- **[Usage Guide](docs/usage.md)** - Installation, workflows, and examples
- **[Architecture Guide](docs/architecture.md)** - Design principles and patterns
- **[Plugins](docs/capabilities/plugins.md)** - Plugin catalog with features and commands
- **[Agents](docs/capabilities/agents.md)** - AI agent personas and expertise
- **[Skills](docs/capabilities/skills.md)** - Knowledge modules and reusability
- **[Commands](docs/capabilities/commands.md)** - Complete command reference

## Contributing

Want to add a new plugin? Use the built-in design tool:

```bash
/marketplace-dev:design-plugin
```

This interactive command will guide you through plugin architecture, identify reusable skills, and generate an implementation plan.

For detailed contribution guidelines, see [Architecture Guide](docs/architecture.md).

## Bugs & Enhancements

Found a bug or have a feature request? Please report it via [GitHub Issues](https://github.com/bradleyboehmke/brads-marketplace/issues).

## License

Personal use only.
