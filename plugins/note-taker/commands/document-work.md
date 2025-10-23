---
description: Helps documenting project work in my personal notes system.
---

# Document Work

Guide the user through creating a structured note from their work session.

## Process

1. **Invoke the documentation-assistant agent** to handle the workflow
2. The agent will:
   - Analyze the Claude Code conversation and git history
   - Ask which organization (84.51 or UC)
   - Dynamically discover and present available templates
   - Let user select template and save location
   - Generate intelligent content proposals for each field
   - Save the completed note

## What the Agent Does

The documentation-assistant is an expert at:
- Extracting information from conversation history (primary source)
- Supplementing with git data (commits, files, messages)
- Generating specific, detailed content for template fields
- Making it easy for users to accept proposals (just press Enter)

The agent has access to skills for:
- **organization-config**: Dynamic template and location discovery
- **content-generation**: Strategies for analyzing work and proposing content

## User Experience

The workflow is conversational and interactive:
1. Select organization and template
2. Choose save location and project name
3. Review and approve proposed content for each field
4. Note is automatically saved

The agent makes intelligent proposals so users can complete documentation quickly with minimal typing.
