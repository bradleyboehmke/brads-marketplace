# Usage Guide

This guide explains how to install and use plugins from Brad's Marketplace.

## Installation

### Adding the Marketplace

To add this marketplace to your Claude Code installation:

```bash
/plugin marketplace add brads-marketplace
```

Or if installing from a local directory:

```bash
/plugin marketplace add /path/to/brads-marketplace
```

### Installing Plugins

Once the marketplace is added, you can install specific plugins:

```bash
/plugin install note-taker
```

To see all available plugins:

```bash
/plugin list
```

## Using the note-taker Plugin

The note-taker plugin helps you document your project work by creating structured notes based on templates.

### Basic Workflow

1. **Complete your work** - Make commits, write code, have discussions with Claude Code

2. **Start the documentation process:**
   ```bash
   /note-taker:document-work
   ```

3. **Follow the interactive prompts:**
   - The plugin will analyze today's git commits and conversation history
   - Select your organization (84.51 or UC)
   - Choose the appropriate template for your work type
   - Select where to save the note
   - Provide a project name for the filename

4. **Review proposed content:**
   - The plugin will generate content for each template field based on:
     - Your Claude Code conversation (primary source)
     - Git commits and changes (supplementary)
   - You can accept, edit, or add to each proposed field
   - Simply press Enter to accept the default proposal

5. **Save the note:**
   - The plugin will save your note to the appropriate location
   - Format: `/Desktop/Notes/{org}/{subdirectory}/{YYYY-MM-DD}-{project-name}.md`

### Tips for Best Results

- **Use descriptive commit messages** - They help the plugin understand what you did
- **Complete logical units of work** - Document after finishing a feature or task
- **Leverage conversation context** - The plugin can see everything discussed in the Claude Code session
- **Customize proposals** - Don't hesitate to edit the suggested content to add details
- **Press Enter to accept** - If the proposal looks good, just hit Enter to move on

### Example Session

```
You: /note-taker:document-work

Claude: I've analyzed your work today. I can see you:
- Enhanced the document-work plugin with conversation context
- Updated marketplace architecture
- Made 2 commits with changes to 3 files

Which organization is this work for?
1. 84.51
2. UC

You: 1

Claude: Here are the available templates for 84.51:
1. obj4-genai-coding-template.md
2. build-log-template.md
[... more templates ...]

Which template would you like to use?

You: 1

[... continues with interactive prompts ...]
```

## Customization

### Adding Custom Templates

To add your own templates:

1. Create a new template in `/Users/b294776/Desktop/Notes/templates/`
2. Use the format: `{org}-{name}-template.md` (e.g., `8451-new-template.md`)
3. Update the plugin's `document-work.md` command file to include your new template

### Adding New Subdirectories

To add new save locations:

1. Create the subdirectory in `/Users/b294776/Desktop/Notes/{org}/`
2. Update the plugin's `document-work.md` command file to include the new location

## Troubleshooting

### Plugin not found
If the plugin isn't recognized after installation, try:
```bash
/plugin refresh
```

### Git commands failing
Ensure you're in a git repository when running the document-work command. The plugin works without git, but provides richer context when git history is available.

### Template not found
Verify that the template file exists in `/Users/b294776/Desktop/Notes/templates/` and that the filename matches exactly what's listed in the plugin.

## Getting Help

For issues or questions:
1. Check this documentation
2. Review the plugin source code in `plugins/note-taker/`
3. Open an issue in the marketplace repository
