---
description: Helps documenting project work in my personal notes system.
---

# Document Work

Guide the user through creating a structured note from their work session using an interactive, numbered-option workflow.

## Process

1. **Invoke the documentation-assistant agent** to handle the workflow
2. The agent will guide you through 6 steps with easy numbered selections

## Interactive Workflow Steps

### Step 1: Organization Selection
Present three numbered options:
- [1] 84.51
- [2] University of Cincinnati
- [3] Content Creation

### Step 2: Template Selection
- Dynamically discover all templates in `/Users/b294776/Desktop/Notes/templates/`
- Filter by organization:
  - 84.51: obj*, annual-objectives*, weekly-5-15*, etc. (excludes uc-*, content-*, paper-*, build-log*)
  - UC: uc-* templates only
  - Content Creation: content-*, paper-*, build-log* templates only
- Present numbered list of available templates
- User enters number to select

### Step 3: Note Name
- Agent proposes an intelligent name based on conversation context
- User can type [1] to accept or type alternative name

### Step 4: Save Directory
- Dynamically discover subdirectories in organization folder
  - For 84.51: `/Users/b294776/Desktop/Notes/8451/`
  - For UC: `/Users/b294776/Desktop/Notes/uc/`
  - For Content Creation: `/Users/b294776/Desktop/Notes/content/`
- Present numbered list of directories
- User enters number to select

### Step 5: Template Field Content
For each field in the template:
- Agent proposes intelligent content based on conversation and git history
- User can type [1] to accept or type alternative content
- Repeat for all template fields

### Step 6: Save
- Build full path: `/Users/b294776/Desktop/Notes/{org}/{directory}/{date}-{name}.md`
- Save the completed note
- Confirm with user showing full path

## What the Agent Does

The documentation-assistant is an expert at:
- Extracting information from conversation history (primary source)
- Supplementing with git data (commits, files, messages)
- Generating specific, detailed content for template fields
- Proposing intelligent defaults for names and content
- Making it easy for users to accept proposals (just type `1`)

The agent has access to skills for:
- **organization-config**: Template locations and organization configuration
- **content-generation**: Strategies for analyzing work and proposing content

## User Experience

The workflow uses numbered options throughout for fast, easy selection:
- Type `1`, `2`, or `3` to select organization
- Type a number to select template
- Type `1` to accept proposed note name (or type alternative)
- Type a number to select save directory
- Type `1` to accept each field's content (or type alternative)

This makes documentation fast and effortless - most users will just type `1` repeatedly to accept good proposals.
