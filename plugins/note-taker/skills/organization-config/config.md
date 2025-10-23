# Organization Configuration

This skill provides configuration for different organizations including template locations and save directories.

## Base Paths

**Templates Base Directory:** `/Users/b294776/Desktop/Notes/templates/`
**Notes Base Directory:** `/Users/b294776/Desktop/Notes/`

## Organizations

### 84.51

**Templates Location:** `/Users/b294776/Desktop/Notes/templates/`
**Notes Subdirectory:** `8451/`

**Template Discovery:**
Use Glob to find all templates, then filter for 84.51-specific ones:
```
Glob pattern: /Users/b294776/Desktop/Notes/templates/*.md
```
Include templates that match these patterns:
- Start with `obj` (e.g., obj1-team-development-template.md, obj4-genai-coding-template.md)
- Start with `annual-objectives`
- Start with `weekly-5-15`
- Start with `quarterly-metrics`
- Start with `hiring-interview`
- Start with `1on1`
- Start with `team-meeting`
- Start with `tech-lt-meeting`
- Start with `labs-lt-meeting`
- Start with `quality-review`

Exclude templates that start with `uc-`, `content-`, `paper-`, or `build-log`

**Save Locations Discovery:**
Use Bash to dynamically list all subdirectories:
```bash
ls -d /Users/b294776/Desktop/Notes/8451/*/
```

### UC (University of Cincinnati)

**Templates Location:** `/Users/b294776/Desktop/Notes/templates/`
**Notes Subdirectory:** `uc/`

**Template Discovery:**
Use Glob to find all UC templates (files that start with "uc-"):
```
Glob pattern: /Users/b294776/Desktop/Notes/templates/uc-*.md
```

**Save Locations Discovery:**
Use Bash to dynamically list all subdirectories:
```bash
ls -d /Users/b294776/Desktop/Notes/uc/*/
```

### Content Creation

**Templates Location:** `/Users/b294776/Desktop/Notes/templates/`
**Notes Subdirectory:** `content/`

**Template Discovery:**
Use Glob to find all content creation templates:
```
Glob pattern: /Users/b294776/Desktop/Notes/templates/*.md
```
Include templates that match these patterns:
- Start with `content-` (e.g., content-idea-template.md)
- Start with `paper-` (e.g., paper-notes-template.md)
- Start with `build-log`

**Save Locations Discovery:**
Use Bash to dynamically list all subdirectories:
```bash
ls -d /Users/b294776/Desktop/Notes/content/*/
```
If the content/ directory doesn't exist yet, create it first.

## Dynamic Discovery Guidelines

### Step 1: Organization Selection
Present numbered options:
```
[1] 84.51
[2] University of Cincinnati
[3] Content Creation
```

### Step 2: Finding Templates
1. Use Glob to get all templates: `/Users/b294776/Desktop/Notes/templates/*.md`
2. Filter based on organization selected:
   - **84.51**: Include templates matching 84.51 patterns, exclude uc-*, content-*, paper-*, build-log*
   - **UC**: Include only templates starting with `uc-`
   - **Content**: Include only templates starting with `content-`, `paper-`, or `build-log`
3. Extract clean display names from filenames:
   - Remove directory path
   - Remove `-template.md` suffix
   - Remove `.md` extension
   - Convert hyphens to spaces for display
   - Capitalize appropriately
4. Present as numbered list:
```
Available templates:
[1] Obj4 Genai Coding
[2] Weekly 5 15
[3] Annual Objectives Note
...
```

**Example:**
- File: `/Users/b294776/Desktop/Notes/templates/obj4-genai-coding-template.md`
- Display as: `[1] Obj4 Genai Coding`

### Step 3: Propose Note Name
1. Analyze conversation context to generate intelligent name
2. Format: lowercase with hyphens (e.g., "marketplace-schema-update")
3. Present with acceptance option:
```
Proposed note name: "marketplace-schema-update"

[1] Accept this name
Or type alternative name:
```

### Step 4: Finding Save Locations
1. Use Bash `ls -d` to list subdirectories under the organization folder:
   - **84.51**: `/Users/b294776/Desktop/Notes/8451/*/`
   - **UC**: `/Users/b294776/Desktop/Notes/uc/*/`
   - **Content**: `/Users/b294776/Desktop/Notes/content/*/`
2. Extract directory names (remove path and trailing slash)
3. Present as numbered list:
```
Where should this note be saved?
[1] obj4-genai-coding
[2] cross-cutting
[3] weekly-reports
...
```

**Example bash command:**
```bash
ls -d /Users/b294776/Desktop/Notes/8451/*/ | sed 's|.*/||' | sed 's|/$||'
```

### Step 5: Building Save Paths
Format: `{notes_base}/{org_subdir}/{save_location}/{date}-{note-name}.md`

**Components:**
- `notes_base`: `/Users/b294776/Desktop/Notes/`
- `org_subdir`: `8451/`, `uc/`, or `content/`
- `save_location`: Selected directory name
- `date`: Today's date in YYYY-MM-DD format
- `note-name`: User-confirmed name in lowercase-hyphenated format

**Examples:**
- `/Users/b294776/Desktop/Notes/8451/obj4-genai-coding/2025-10-23-marketplace-schema-update.md`
- `/Users/b294776/Desktop/Notes/uc/course-development/2025-10-23-chapter-3-updates.md`
- `/Users/b294776/Desktop/Notes/content/blog-posts/2025-10-23-new-article-idea.md`

## Template Processing

### Reading Templates
1. After user selects template number, use Read tool to load the template file
2. Identify all fields that need to be filled
3. Look for patterns like:
   - `{{field_name}}`
   - `## Field Name`
   - Placeholder text or prompts

### Filling Template Fields
For each field identified:
1. Generate intelligent content based on conversation history and git data
2. Present proposed content with acceptance option:
```
[Field Name]:
Proposed content here...

[1] Accept this content
Or type alternative content:
```

3. If user types `1`, use the proposed content
4. If user types anything else, use their typed content instead

## Workflow Summary

When invoked, follow this exact sequence:

1. **Organization Selection** → User selects [1], [2], or [3]
2. **Template Discovery** → Glob for templates → Filter by organization → Present numbered list
3. **Template Selection** → User selects template number
4. **Name Proposal** → Propose name → User types [1] or alternative
5. **Directory Discovery** → List directories → Present numbered list
6. **Directory Selection** → User selects directory number
7. **Template Loading** → Read template file
8. **Field Iteration** → For each field:
   - Propose content
   - User types [1] or alternative
9. **Save Note** → Write to final path
10. **Confirm** → Show user the full path where note was saved
