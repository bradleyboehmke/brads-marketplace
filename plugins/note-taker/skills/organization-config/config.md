# Organization Configuration

This skill provides configuration for different organizations including template locations and save directories.

## Base Paths

**Templates Directory:** `/Users/b294776/Desktop/Notes/templates/`
**Notes Base Directory:** `/Users/b294776/Desktop/Notes/`

## Organizations

### 84.51

**Templates Prefix:** `8451-` or no prefix for legacy templates
**Notes Subdirectory:** `8451/`

**Available Save Locations:**
- annual-objectives
- cross-cutting
- obj1-team-development
- obj2-tech-lt
- obj3-standards
- obj4-genai-coding
- obj5-labsmate
- obj6-procurement
- open-roles
- weekly-reports

**Template Discovery:**
Use Glob to find templates dynamically:
```
Glob pattern: /Users/b294776/Desktop/Notes/templates/8451-*.md
Glob pattern: /Users/b294776/Desktop/Notes/templates/*-template.md (exclude uc-*)
```

### UC (University of Cincinnati)

**Templates Prefix:** `uc-`
**Notes Subdirectory:** `uc/`

**Available Save Locations:**
- course-development
- program-director
- weekly-notes

**Template Discovery:**
Use Glob to find templates dynamically:
```
Glob pattern: /Users/b294776/Desktop/Notes/templates/uc-*.md
```

## Dynamic Discovery Guidelines

### Finding Templates
1. Use Glob tool to discover templates at runtime
2. Filter by organization prefix
3. Present as numbered list to user
4. Extract display names from filenames (remove prefix/suffix)

### Finding Save Locations
1. Use Bash `ls -d` to list subdirectories
2. Present as numbered list to user
3. Use exact directory names for saving

### Building Save Paths
Format: `{notes_base}/{org_subdir}/{save_location}/{date}-{project-name}.md`

Examples:
- `/Users/b294776/Desktop/Notes/8451/obj4-genai-coding/2025-10-22-plugin-refactor.md`
- `/Users/b294776/Desktop/Notes/uc/weekly-notes/2025-10-22-week-summary.md`

## Usage Instructions

When helping users document work:
1. Ask which organization (84.51 or UC)
2. Discover templates dynamically using Glob
3. Let user select template
4. Discover save locations dynamically using Bash
5. Let user select save location
6. Ask for project name
7. Build full save path using the format above
