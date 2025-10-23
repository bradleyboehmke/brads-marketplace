# Marketplace.json Schema Skill

This skill provides comprehensive knowledge of the marketplace.json schema and formatting standards for Claude Code plugin marketplaces.

## Purpose

Provides agents and commands with detailed understanding of:
- Marketplace.json structure and required fields
- Plugin metadata standards
- Proper formatting conventions
- Best practices for plugin registration

## When to Use

Load this skill when:
- Creating new plugins
- Updating marketplace.json
- Adding plugin metadata
- Validating plugin configurations
- Registering plugins in the marketplace

## Schema Structure

### Top-Level Structure

```json
{
  "name": "marketplace-name",
  "owner": { ... },
  "metadata": { ... },
  "plugins": [ ... ]
}
```

### Owner Object

**Required fields:**
```json
"owner": {
  "name": "Full Name",
  "email": "email@example.com",
  "url": "https://github.com/username"
}
```

**Field Descriptions:**
- `name`: Owner's full name (string)
- `email`: Contact email address (string)
- `url`: GitHub profile or website URL (string)

### Metadata Object

**Required fields:**
```json
"metadata": {
  "description": "Brief description of the marketplace",
  "version": "1.0.0"
}
```

**Field Descriptions:**
- `description`: Clear, concise description of the marketplace's purpose
- `version`: Semantic version number (string, format: MAJOR.MINOR.PATCH)

### Plugin Object

Each plugin in the `plugins` array should follow this structure:

**Required fields:**
```json
{
  "name": "plugin-name",
  "source": "./plugins/plugin-name",
  "description": "Brief description of the plugin",
  "version": "1.0.0",
  "author": {
    "name": "Author Name",
    "url": "https://github.com/username"
  },
  "homepage": "https://github.com/username/repo",
  "repository": "https://github.com/username/repo",
  "license": "MIT",
  "keywords": [
    "keyword1",
    "keyword2",
    "keyword3"
  ],
  "category": "category-name",
  "strict": false,
  "commands": [
    "./commands/command-name.md"
  ],
  "agents": [
    "./agents/agent-name.md"
  ]
}
```

**Field Descriptions:**

**Core Fields:**
- `name` (required): Plugin name in lowercase-hyphenated format (e.g., "note-taker")
- `source` (required): Relative path to plugin directory (e.g., "./plugins/note-taker")
- `description` (required): Brief, clear description of plugin purpose (5-20 words)
- `version` (required): Semantic version number (string, format: MAJOR.MINOR.PATCH)

**Author & Links:**
- `author` (required): Object containing author name and URL
  - `name`: Author's full name
  - `url`: Author's GitHub profile or website
- `homepage` (required): Plugin's homepage URL (typically GitHub repo)
- `repository` (required): Source code repository URL (typically GitHub repo)
- `license` (required): License identifier (e.g., "MIT", "Apache-2.0")

**Categorization:**
- `keywords` (required): Array of searchable keywords (3-10 keywords recommended)
  - Use descriptive, lowercase terms
  - Include domain-specific terms
  - Help with plugin discovery
- `category` (required): Primary category for the plugin
  - Common categories: "productivity", "development", "education", "security", "testing", "documentation"

**Technical:**
- `strict` (required): Boolean flag for strict mode (typically `false`)
  - `true`: Enables stricter validation and error handling
  - `false`: More permissive mode (default)

**Components:**
- `commands` (optional): Array of relative paths to command files
  - Format: `"./commands/command-name.md"`
  - Each command should have its own file
  - At least one command OR agent is required per plugin
- `agents` (optional): Array of relative paths to agent files
  - Format: `"./agents/agent-name.md"`
  - Each agent should have its own file
  - At least one command OR agent is required per plugin

## Complete Example

```json
{
  "name": "brads-marketplace",
  "owner": {
    "name": "Brad Boehmke",
    "email": "boehmkbc@gmail.com",
    "url": "https://github.com/bradleyboehmke"
  },
  "metadata": {
    "description": "Brad's personal collection of Claude Code plugins",
    "version": "1.0.0"
  },
  "plugins": [
    {
      "name": "note-taker",
      "source": "./plugins/note-taker",
      "description": "Automates note-taking by analyzing project work and creating structured notes using templates",
      "version": "1.0.0",
      "author": {
        "name": "Brad Boehmke",
        "url": "https://github.com/bradleyboehmke"
      },
      "homepage": "https://github.com/bradleyboehmke/brads-marketplace",
      "repository": "https://github.com/bradleyboehmke/brads-marketplace",
      "license": "MIT",
      "keywords": [
        "notes",
        "documentation",
        "templates",
        "work-tracking"
      ],
      "category": "productivity",
      "strict": false,
      "commands": [
        "./commands/document-work.md"
      ],
      "agents": [
        "./agents/documentation-assistant.md"
      ]
    }
  ]
}
```

## Field Requirements Summary

### Marketplace Level
- ✅ `name` (string)
- ✅ `owner` (object)
  - ✅ `name` (string)
  - ✅ `email` (string)
  - ✅ `url` (string)
- ✅ `metadata` (object)
  - ✅ `description` (string)
  - ✅ `version` (string)
- ✅ `plugins` (array)

### Plugin Level
- ✅ `name` (string)
- ✅ `source` (string)
- ✅ `description` (string)
- ✅ `version` (string)
- ✅ `author` (object)
  - ✅ `name` (string)
  - ✅ `url` (string)
- ✅ `homepage` (string)
- ✅ `repository` (string)
- ✅ `license` (string)
- ✅ `keywords` (array of strings)
- ✅ `category` (string)
- ✅ `strict` (boolean)
- ⚠️ `commands` (array, optional but recommended)
- ⚠️ `agents` (array, optional but recommended)

**Note:** At least one of `commands` or `agents` should be provided for each plugin.

## Common Categories

Choose the most appropriate category for your plugin:

- **productivity**: Tools for task management, note-taking, workflow automation
- **development**: Software development tools, code generation, refactoring
- **education**: Learning resources, tutorials, course content creation
- **security**: Security analysis, vulnerability scanning, penetration testing
- **testing**: Test automation, test generation, quality assurance
- **documentation**: Documentation generation, API docs, README creation
- **deployment**: CI/CD, deployment automation, release management
- **monitoring**: Application monitoring, logging, observability
- **data**: Data processing, analysis, ETL tools
- **ai**: AI/ML tools, model training, inference

## Keyword Best Practices

**Good Keywords:**
- Specific and descriptive
- Related to plugin functionality
- Common search terms
- Technology-specific terms

**Examples:**
- ✅ "notes", "documentation", "templates", "work-tracking"
- ✅ "kubernetes", "deployment", "containers", "helm"
- ✅ "testing", "automation", "quality", "coverage"

**Bad Keywords:**
- ❌ Generic terms like "tool", "helper", "utility"
- ❌ Redundant with plugin name
- ❌ Marketing terms like "best", "awesome", "amazing"

## Validation Checklist

Before adding a plugin to marketplace.json:

**Structure:**
- [ ] Plugin has unique name
- [ ] Source path points to valid directory
- [ ] All required fields are present
- [ ] JSON is valid and properly formatted

**Metadata:**
- [ ] Description is clear and concise (5-20 words)
- [ ] Version follows semantic versioning (x.y.z)
- [ ] Author information is complete
- [ ] Homepage and repository URLs are valid
- [ ] License is specified

**Categorization:**
- [ ] 3-10 relevant keywords provided
- [ ] Keywords are lowercase and descriptive
- [ ] Category is appropriate
- [ ] No duplicate or redundant keywords

**Components:**
- [ ] At least one command or agent is listed
- [ ] All command paths are valid
- [ ] All agent paths are valid
- [ ] Paths use correct relative format (./commands/... or ./agents/...)

**Consistency:**
- [ ] Naming follows lowercase-hyphenated convention
- [ ] All URLs use HTTPS
- [ ] Author info matches marketplace owner (if applicable)
- [ ] License matches LICENSE file in repository

## Common Mistakes to Avoid

1. **Missing Required Fields:**
   - Forgetting to add `version`, `author`, or `keywords`
   - Solution: Use this skill as a reference checklist

2. **Invalid Paths:**
   - Using absolute paths instead of relative
   - Incorrect file extensions (.md vs .markdown)
   - Solution: Use `./` prefix and verify files exist

3. **Inconsistent Naming:**
   - Mixing camelCase and kebab-case
   - Using uppercase in plugin names
   - Solution: Always use lowercase-hyphenated format

4. **Poor Descriptions:**
   - Too vague: "A helpful tool"
   - Too verbose: Multiple sentences
   - Solution: 5-20 words, clear purpose statement

5. **Invalid JSON:**
   - Missing commas
   - Trailing commas
   - Unquoted strings
   - Solution: Use JSON validator or linter

## Adding a New Plugin

When adding a new plugin to marketplace.json:

1. **Copy Template:**
   ```json
   {
     "name": "plugin-name",
     "source": "./plugins/plugin-name",
     "description": "Brief description",
     "version": "1.0.0",
     "author": {
       "name": "Your Name",
       "url": "https://github.com/yourusername"
     },
     "homepage": "https://github.com/yourusername/repo",
     "repository": "https://github.com/yourusername/repo",
     "license": "MIT",
     "keywords": ["keyword1", "keyword2", "keyword3"],
     "category": "category-name",
     "strict": false,
     "commands": [],
     "agents": []
   }
   ```

2. **Fill in Details:**
   - Update name, description, keywords, category
   - Add command and/or agent paths
   - Verify all URLs

3. **Validate:**
   - Run through validation checklist
   - Check JSON syntax
   - Verify paths exist

4. **Test:**
   - Restart Claude Code to load new plugin
   - Test commands and agents work
   - Verify metadata displays correctly

## Version Management

Follow semantic versioning for both marketplace and plugins:

**Format:** MAJOR.MINOR.PATCH

- **MAJOR**: Breaking changes, incompatible API changes
- **MINOR**: New features, backward-compatible additions
- **PATCH**: Bug fixes, backward-compatible fixes

**Examples:**
- `1.0.0`: Initial release
- `1.1.0`: Added new command
- `1.1.1`: Fixed bug in existing command
- `2.0.0`: Restructured plugin (breaking change)

## References

- [Semantic Versioning](https://semver.org/)
- [SPDX License List](https://spdx.org/licenses/)
- [JSON Schema Specification](https://json-schema.org/)
