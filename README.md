# Brad's Claude Code Marketplace

Personal collection of general-purpose Claude Code plugins for productivity and workflow automation.

## Overview

This marketplace follows a modular, single-purpose plugin architecture optimized for minimal token usage and maximum composability. Each plugin is focused on solving one specific problem well.

## Repository Structure

```
brads-marketplace/
├── .claude-plugin/
│   └── marketplace.json          # Plugin marketplace configuration
├── plugins/
│   ├── note-taker/               # Documentation plugin
│   │   └── commands/
│   │       └── document-work.md
│   └── marketplace-dev/          # Plugin development tools
│       ├── agents/
│       │   └── plugin-architect.md
│       ├── commands/
│       │   ├── create-plugin.md
│       │   └── validate-plugin.md
│       └── skills/
│           ├── architecture-principles/
│           └── plugin-templates/
├── docs/                          # Comprehensive documentation
│   ├── plugins.md                 # Plugin documentation
│   └── usage.md                   # Usage guide
└── README.md                      # This file
```

## Available Plugins

### note-taker

Creates structured notes from project work using pre-defined templates.

**Usage:** `/note-taker:document-work`

**What it does:**
- Analyzes your Claude Code conversation history and git commits
- Guides you through selecting the right template for your work
- Intelligently proposes content for each template field based on your work
- Saves the note to the appropriate location in your Notes directory

**Key Features:**
- Leverages conversation context as primary source of information
- Supports multiple template types for different use cases
- Interactive field-by-field content proposal and approval
- Automatic filename generation with date stamps

**Workflow:**
1. Run `/note-taker:document-work` after completing your work
2. Answer prompts about template and save location
3. Review and approve (or edit) proposed content for each field
4. Note is automatically saved with format: `YYYY-MM-DD-project-name.md`

### marketplace-dev

Tools and expertise for building plugins that align with marketplace architecture.

**Usage:** `/marketplace-dev:create-plugin` or `/marketplace-dev:validate-plugin`

**What it does:**
- Guides you through creating new plugins following architecture principles
- Validates existing plugins for compliance with best practices
- Provides expert guidance on plugin design and structure
- Includes comprehensive templates and examples

**Key Features:**
- Plugin Architect agent for design consultation
- Interactive plugin scaffolding
- Comprehensive architecture validation
- Skills for architecture principles and templates
- Ensures single responsibility and composability

**Components:**
- `plugin-architect` agent - Expert in marketplace architecture
- `create-plugin` command - Scaffold new plugins interactively
- `validate-plugin` command - Validate plugin compliance
- `architecture-principles` skill - Deep knowledge of design patterns
- `plugin-templates` skill - Ready-to-use templates

## Installation

### Adding the Marketplace

To add this marketplace to your Claude Code installation:

```bash
/plugin marketplace add brads-marketplace
```

Or from a local directory:

```bash
/plugin marketplace add /path/to/brads-marketplace
```

### Installing Plugins

Once the marketplace is added, install specific plugins:

```bash
/plugin install note-taker
```

View all available plugins:

```bash
/plugin list
```

## Documentation

For detailed information:
- [Plugin Documentation](docs/plugins.md) - Detailed information about each plugin
- [Usage Guide](docs/usage.md) - Comprehensive guide on installation and usage

## Architecture Principles

This marketplace follows these design principles inspired by best practices:

1. **Single Responsibility** - Each plugin does one thing well
2. **Minimal Token Usage** - Lightweight components that load only what's needed
3. **Composable** - Plugins can work independently or together
4. **Progressive Disclosure** - Load metadata first, instructions when activated, resources on demand

## Adding New Plugins

To add a new plugin:

1. Create a new directory under `plugins/`:
   ```
   plugins/your-plugin-name/
   ├── commands/        # Slash commands
   ├── agents/          # (optional) AI agents
   └── skills/          # (optional) Agent skills
   ```

2. Add to `.claude-plugin/marketplace.json`:
   ```json
   {
     "name": "your-plugin-name",
     "source": "./plugins/your-plugin-name",
     "description": "Brief description"
   }
   ```

3. Document in `docs/plugins.md`

## License

Personal use only.
