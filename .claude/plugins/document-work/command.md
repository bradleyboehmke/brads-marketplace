You are helping the user document their project work by creating a structured note based on their work templates.

## Your Task

Guide the user through an interactive conversation to:
1. Analyze today's git commits in the current repository
2. Select the appropriate organization and template
3. Fill in the template with information about their work
4. Save the note in the correct location

## Step-by-Step Process

### Step 1: Analyze Today's Work

First, analyze the git repository to understand what work was done today:
- Run `git log --since="today" --pretty=format:"%h - %s (%an)" --no-merges` to see today's commits
- Run `git diff --name-only HEAD@{1.day.ago}..HEAD` to see changed files (or use appropriate method to see today's changes)
- Summarize the work based on commits and file changes

If there are no commits today or the directory is not a git repository, inform the user and ask them to describe the work they did.

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

### Step 6: Read Template and Fill It In

Use the Read tool to read the selected template file from the templates directory.

Then, go through an interactive conversation to fill in the template:
1. Auto-fill fields you can determine:
   - Date (today's date)
   - Any information from git analysis (progress, work done, files changed)
2. For required fields (check VALIDATION RULES comments in template):
   - Ask the user for each required field
   - Wait for response before moving to next field
3. Explain to the user what you've pre-filled and what still needs their input

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
- Don't rush - wait for user responses at each decision point
- Use today's date in YYYY-MM-DD format for both the filename and date field
- Read the actual template file to ensure you're using the correct structure
- Pay attention to VALIDATION RULES in template comments to ensure required fields are filled
- If git analysis fails, proceed anyway and gather information through conversation
- Keep the user informed about what you're doing at each step
