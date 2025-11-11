---
title: Marketplace Registration Standards
description: Plugin registration, versioning, tagging, and quality gates for marketplace
tags: [registration, versioning, quality, marketplace]
---

# Marketplace Registration Standards

## Metadata

**Purpose**: Define registration process and quality standards for marketplace plugins
**Applies to**: All Personal marketplace plugins
**Version**: 1.0.0

---

## Instructions

### Marketplace Registration

**marketplace.json Entry**:
```json
{
  "name": "brads-marketplace",
  "description": "Personal Custom Claude Plugins",
  "owner": {
    "name": "Personal Team"
  },
  "plugins": [
    {
      "name": "plugin-name",
      "source": "./plugin-name",
      "description": "Plugin description from plugin.json"
    }
  ]
}
```

**Registration Process**:
1. Create plugin in its own directory
2. Add entry to root `marketplace.json`
3. Description should match `plugin.json`
4. Source is relative path from marketplace root

### Documentation Standards

**Plugin README** (if plugin is complex):
- Purpose and use cases
- Installation instructions
- Command reference
- Examples

**Root CLAUDE.md** (marketplace-level):
- Update with new plugin info
- Add example commands
- Note any cross-plugin workflows

### Version Management

**Semantic Versioning**:
- `1.0.0` - Initial release
- `1.1.0` - New commands/features (minor)
- `1.0.1` - Bug fixes (patch)
- `2.0.0` - Breaking changes (major)

**What triggers major version**:
- Removing commands
- Changing command parameters (breaking)
- Restructuring that affects users

**What triggers minor version**:
- Adding new commands
- Adding new skills
- Adding new agents
- New features (non-breaking)

**What triggers patch version**:
- Bug fixes
- Documentation updates
- Performance improvements
- Refactoring (no user-facing changes)

### Quality Gates

Before adding plugin to marketplace:
- [ ] plugin.json with all required fields
- [ ] All files have proper frontmatter
- [ ] Commands follow output parameter standards
- [ ] Purpose describable in 5-10 words
- [ ] Entry added to marketplace.json
- [ ] CLAUDE.md updated with examples
- [ ] Tested with `claude plugins install ./plugin-name`

**Additional quality checks**:
- [ ] No duplicate knowledge across components
- [ ] Skills use progressive disclosure (if applicable)
- [ ] Component sizes within guidelines (agents <500, skills <400, commands <600 lines)
- [ ] Clear separation of concerns (agent vs skill vs command)

### Personal Tags

Use these tags in plugin.json for discoverability:

**Domain Tags**:
- `standards` - Validation/compliance plugins
- `investigation` - Analysis/discovery plugins
- `development` - Dev tool plugins
- `documentation` - Doc generation/validation

**Function Tags**:
- `validation` - Checks compliance
- `analysis` - Analyzes code/architecture
- `generation` - Creates artifacts
- `orchestration` - Coordinates workflows

**Context Tags**:
- `labs` - Labs-specific
- `python` - Python projects
- `data-science` - ML/DS projects
- `architecture` - System design

**Technology Tags**:
- `mlflow` - MLflow integration
- `databricks` - Databricks integration
- `spark` - Apache Spark
- `pytest` - Testing with pytest
- `poetry` - Poetry package management

### Plugin Lifecycle

**Development Phase**:
- Version: `0.x.x`
- Status: Experimental
- Can make breaking changes frequently
- Not recommended for production use

**Stable Phase**:
- Version: `1.x.x+`
- Status: Stable
- Follow semantic versioning strictly
- Breaking changes only in major versions

**Deprecated Phase**:
- Mark in plugin.json: `"deprecated": true`
- Document migration path in README
- Provide timeline for removal
- Suggest alternative plugins

---

## Resources

### Complete marketplace.json Example

```json
{
  "name": "brads-marketplace",
  "description": "Personal Custom Claude Plugins",
  "version": "1.0.0",
  "owner": {
    "name": "Personal Team",
    "url": "https://github.com/USERNAME"
  },
  "plugins": [
    {
      "name": "validator",
      "source": "./validator",
      "description": "Standards validator for personal use projects",
      "tags": ["standards", "validation", "personal"]
    },
    {
      "name": "repo-investigator",
      "source": "./repo-investigator",
      "description": "Repository analysis and investigation tools",
      "tags": ["investigation", "analysis", "personal"]
    },
    {
      "name": "document-generator",
      "source": "./document-generator",
      "description": "Architecture documentation generation tools",
      "tags": ["documentation", "generation", "personal"]
    },
    {
      "name": "marketplace-dev",
      "source": "./marketplace-dev",
      "description": "Plugin development and architecture tools",
      "tags": ["development", "architecture", "personal"]
    }
  ]
}
```

### Plugin Release Checklist

**Before 1.0.0 Release**:
- [ ] All features implemented and tested
- [ ] Documentation complete
- [ ] Examples provided
- [ ] Quality gates passed
- [ ] Peer review completed
- [ ] Breaking changes documented
- [ ] Migration guide (if replacing existing plugin)

**For Minor Version Release (1.x.0)**:
- [ ] New features tested
- [ ] Documentation updated
- [ ] Backward compatibility verified
- [ ] Examples updated
- [ ] CHANGELOG.md updated

**For Patch Version Release (1.0.x)**:
- [ ] Bug fixes tested
- [ ] No breaking changes
- [ ] Documentation updated (if needed)
- [ ] CHANGELOG.md updated

### Deprecation Notice Template

Add to plugin README.md:

```markdown
## ⚠️ Deprecation Notice

This plugin is deprecated as of [date] and will be removed in [future date].

**Reason**: [Why this plugin is being deprecated]

**Migration Path**:
- Use [alternative-plugin] instead
- Migration guide: [link or instructions]
- Support timeline: [when support ends]

**Questions**: Contact Personal team
```

### Version History Template

Add to plugin README.md or CHANGELOG.md:

```markdown
## Version History

### v2.0.0 (2024-01-15)
**Breaking Changes**:
- Removed deprecated command `/old-command`
- Changed parameter format for `/main-command`

**New Features**:
- Added `/new-command` for improved workflow
- New skill: `advanced-analysis.md`

**Migration Guide**:
- Replace `/old-command` with `/new-command --mode=legacy`
- Update parameter: `--old-param` → `--new-param`

### v1.2.0 (2024-01-01)
**New Features**:
- Added support for Python 3.12
- New skill: `python-312-features.md`

**Bug Fixes**:
- Fixed issue with virtual environment detection

### v1.1.0 (2023-12-15)
**New Features**:
- Added `/quick-check` command
- Performance improvements

### v1.0.0 (2023-12-01)
**Initial stable release**
- Core validation features
- Documentation generation
- CLI integration
```
