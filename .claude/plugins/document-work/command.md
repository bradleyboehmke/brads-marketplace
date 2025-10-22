You are helping the user document their project work by creating a structured note based on their work templates.

## Your Task

Guide the user through an interactive conversation to:
1. Analyze today's git commits in the current repository
2. Select the appropriate organization and template
3. Fill in the template with information about their work
4. Save the note in the correct location

## Step-by-Step Process

### Step 1: Analyze Today's Work

Analyze the work done in this session using multiple sources:

**Primary Source - Claude Code Context:**
- Review the conversation history in this Claude Code session
- Identify key activities: code written, problems solved, features implemented
- Note important decisions, discussions, and design choices
- Extract specific technical details and outcomes
- Identify challenges encountered and how they were resolved

**Secondary Source - Git Repository:**
- Run `git log --since="today" --pretty=format:"%h - %s (%an)" --no-merges` to see today's commits
- Run `git diff --name-only HEAD@{1.day.ago}..HEAD` to see changed files
- Use git data to supplement and validate the Claude conversation analysis

**Synthesis:**
Combine both sources to create a comprehensive understanding of:
- What was built/created
- How it was approached
- What challenges were faced
- What decisions were made
- What outcomes were achieved

If there are no commits today or the directory is not a git repository, rely primarily on the Claude Code conversation context.

### Step 2: Select Organization

Ask the user which organization this work is for:
1. 84.51
2. UC

Wait for their response before proceeding.

### Step 3: Select Template

Based on the organization chosen, list the available templates:

**For 84.51** (templates in `/Users/b294776/Desktop/Notes/templates/8451-templates/`):
- coaching-notes-template.md
- procurement-discovery-template.md
- labs-initiative-template.md
- labs-lt-meeting-template.md
- quarterly-metrics-template.md
- team-meeting-template.md
- quality-review-template.md
- development-plan-template.md
- labsmate-stakeholder-update-template.md
- 1on1-template.md
- procurement-partnership-template.md
- genai-experiment-template.md
- course-session-template.md
- procurement-use-case-template.md
- tech-lt-meeting-template.md

**For UC** (templates in `/Users/b294776/Desktop/Notes/templates/uc-templates/`):
- uc-course-development-template.md
- uc-student-interaction-template.md
- uc-lecture-template.md
- uc-grading-template.md
- uc-weekly-notes-template.md

Display the templates as a numbered list and ask the user to select one. Wait for their response.

### Step 4: Select Save Location

Based on the organization, ask where to save the note:

**For 84.51** (subdirectories of `/Users/b294776/Desktop/Notes/8451/`):
1. obj1-team-development
2. obj2-tech-lt
3. obj3-standards
4. obj4-genai-coding
5. obj5-labsmate
6. obj6-procurement
7. weekly-reports

**For UC** (subdirectories of `/Users/b294776/Desktop/Notes/uc/`):
1. course-development
2. grading
3. lectures
4. program-director
5. student-interactions
6. weekly-notes

Wait for their response.

### Step 5: Choose Filename

Ask the user what project name to use for the filename. Explain that the file will be named: `YYYY-MM-DD-{project-name}.md`

For example: `2025-10-21-labsmate-auth-enhancement.md`

Wait for their response.

### Step 6: Read Template and Propose Content

Use the Read tool to read the selected template file from the templates directory.

Then, intelligently generate content for each template field based on your git analysis:

**Content Generation Strategy:**
1. Use the Claude Code conversation history as the PRIMARY source for understanding the work
2. Supplement with git commits, changed files, and commit messages
3. For each template section, generate thoughtful, specific content based on the combined analysis
4. Present the proposed content to the user and ask if they want to:
   - **Accept** (default - just press Enter)
   - **Edit** (provide modified version)
   - **Add to it** (append additional information)

**Field-by-Field Approach:**
- **Date field:** Auto-fill with today's date (no prompt needed)
- **Title/Experiment Name:** Propose based on project name and work type from conversation
- **Goal:** Extract from the conversation what the user was trying to achieve
- **Approach/How:** Describe the technical approach based on:
  - What was discussed in the Claude conversation
  - Design decisions made during the session
  - Tools and techniques used
  - File changes and commit messages
- **Results/Outcomes:** Summarize what was accomplished based on:
  - Features/code that were successfully implemented
  - Problems that were solved
  - Artifacts that were created
  - Any testing or validation performed
- **Challenges/Blockers:** Extract from conversation any difficulties encountered and how they were resolved
- **Next Steps:** Identify any TODOs, future work, or follow-ups mentioned in the conversation
- **Other template-specific fields:** Generate relevant content based on both conversation and git context

**Presentation Format:**
For each field, show:
```
[Field Name]:
Proposed content here...

Accept this? (Press Enter to accept, or type your changes)
```

**Important:**
- Make proposals specific and detailed, not generic
- Base proposals primarily on the Claude Code conversation context
- Use git data (commits, files, messages) to supplement and validate
- Capture the full richness of the work session: discussions, decisions, iterations, solutions
- If you can't confidently propose content for a field, ask the user for input
- Always explain what you're proposing and why
- Default behavior is acceptance - make it easy to just hit Enter
- The conversation history contains valuable context that git commits don't capture

### Step 7: Generate and Save Note

Once all required information is gathered:
1. Generate the complete note content with the filled template
2. Use the Write tool to save it to: `/Users/b294776/Desktop/Notes/{org}/{subdirectory}/{date}-{project-name}.md`
   - For 84.51: `/Users/b294776/Desktop/Notes/8451/{subdirectory}/{date}-{project-name}.md`
   - For UC: `/Users/b294776/Desktop/Notes/uc/{subdirectory}/{date}-{project-name}.md`
3. Confirm the save location to the user
4. Show a summary of what was documented

## Important Notes

- Be conversational and friendly
- **Leverage the conversation history** - this is your richest source of information about what was done
- Generate intelligent, specific content based on the full session context - don't be generic
- Capture not just WHAT was done, but WHY and HOW based on the conversation
- Make it easy for users to accept good proposals (just press Enter)
- Use today's date in YYYY-MM-DD format for both the filename and date field
- Read the actual template file to ensure you're using the correct structure
- Pay attention to VALIDATION RULES in template comments to ensure required fields are filled
- Git commits supplement the conversation but shouldn't be the primary source
- Keep the user informed about what you're doing at each step
- The goal is to minimize user typing while maintaining quality and accuracy
- You have full context of this work session - use it to create comprehensive documentation
