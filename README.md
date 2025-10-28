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

| Plugin | Description | Documentation |
|--------|-------------|---------------|
| **note-taker** | Automates note-taking by analyzing project work and creating structured notes using templates | [Details](docs/plugins.md#note-taker) |
| **marketplace-dev** | Tools and expertise for building plugins that align with marketplace architecture | [Details](docs/plugins.md#marketplace-dev) |
| **course-builder** | Create educational content for data science courses including chapters, quizzes, notebooks, and slides | [Details](docs/plugins.md#course-builder) |

For comprehensive information about each plugin, including features, commands, and usage examples, see the [Plugin Documentation](docs/plugins.md).

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
