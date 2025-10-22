# Brad's Claude Code Plugins

Personal collection of Claude Code plugins for documenting and managing work at 84.51 and University of Cincinnati.

## Plugins

### document-work

Creates structured notes from project work using pre-defined templates.

**Usage:** `/document-work`

**What it does:**
- Analyzes today's git commits in your current repository
- Guides you through selecting the right organization (84.51 or UC) and template
- Interactively fills in template fields with your input
- Saves the note to the appropriate location in your Notes directory

**Workflow:**
1. Run `/document-work` in any repository where you've done work
2. Answer prompts about organization, template, and save location
3. Fill in required template fields through conversation
4. Note is automatically saved with filename format: `YYYY-MM-DD-project-name.md`

**Note Locations:**
- 84.51 notes: `/Users/b294776/Desktop/Notes/8451/{objective}/`
- UC notes: `/Users/b294776/Desktop/Notes/uc/{category}/`

**Templates Used:**
- 84.51: Uses templates from `/Users/b294776/Desktop/Notes/templates/8451-templates/`
- UC: Uses templates from `/Users/b294776/Desktop/Notes/templates/uc-templates/`

## Installation

To use these plugins in Claude Code:

1. Clone this repository to your local machine
2. In Claude Code settings, add this directory as a plugin source
3. Reload Claude Code to activate the plugins

## Plugin Development

This repository is structured to make it easy to add new plugins:

```
brads-marketplace/
├── .claude/
│   └── plugins/
│       └── document-work/
│           ├── plugin.json
│           └── command.md
└── README.md
```

To add a new plugin, create a new directory under `.claude/plugins/` with the appropriate plugin files.

## License

Personal use only.
