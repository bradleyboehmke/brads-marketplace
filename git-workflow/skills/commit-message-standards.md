---
title: Commit Message Standards
description: Standard commit message format and quality expectations
tags: [git, commits, standards, conventions, conventional-commits]
---

# Commit Message Standards

## Metadata

**Purpose**: Define Standard commit message format and quality expectations
**Applies to**: All Git commits in projects
**Version**: 1.0.0

---

## Instructions

### Conventional Commits Format

All commits must follow the **Conventional Commits** specification:

```
<type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

### Required Elements

**Type** (required): Indicates the kind of change
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `refactor`: Code refactoring (no functional changes)
- `test`: Adding or updating tests
- `chore`: Maintenance tasks (dependencies, tooling)
- `perf`: Performance improvements
- `style`: Code style changes (formatting, whitespace)
- `ci`: CI/CD configuration changes

**Scope** (optional but recommended): Component or module affected
- Examples: `auth`, `api`, `ui`, `database`, `config`
- Keep lowercase and concise

**Subject** (required): Clear, concise description
- Use imperative mood ("add" not "added" or "adds")
- Start with lowercase letter
- No period at the end
- Maximum 50 characters
- Be specific about what changed

### Quality Criteria

**✅ Good commit messages**:
- Clearly communicate intent and context
- Answer: "What does this commit do and why?"
- Use specific, descriptive language
- Focus on the "why" not just the "what"

**❌ Prohibited patterns**:
- Vague messages: "fix bug", "update code", "changes"
- WIP commits: "wip", "work in progress", "temp"
- Generic messages: "fixes", "updates", "misc"
- All caps: "FIX BUG IN LOGIN"
- Emoji without clear text (text is primary, emoji optional)

### Character Limits

- **Subject line**: ≤50 characters (ideal), ≤72 characters (hard limit)
- **Body lines**: Wrap at 72 characters
- **Blank line**: Always separate subject from body

### Issue Linking Policy

**When issue references are required**:
- `feat` - New features (REQUIRED)
- `fix` - Bug fixes (REQUIRED)
- Breaking changes (REQUIRED)
- `refactor` - Large refactorings (RECOMMENDED)
- `perf` - Performance improvements (RECOMMENDED)

**When issue references are optional**:
- `docs` - Documentation-only changes
- `chore` - Dependency updates, tooling
- `test` - Test-only changes
- `style` - Formatting-only changes

**Format in footer**:
- `Closes #123` - Closes an issue (for features, completed work)
- `Fixes #456` - Fixes a bug (for bug fixes)
- `Relates to #789` - Related but doesn't close (for partial work)
- `Refs #101, #102` - References multiple issues

**If no issue exists**:
- Create one first for features/bugs
- OR provide detailed context in commit body explaining why no issue

**Examples**:
```
feat(api): add customer export endpoint

Closes #234
```

```
fix(auth): resolve session timeout on mobile

Multiple users reported session timeouts after 5 minutes of inactivity
on mobile devices. Root cause was aggressive token expiration settings.

Fixes #456
```

### Examples

**Good examples**:

```
feat(auth): add two-factor authentication support

Implements TOTP-based 2FA for user accounts to enhance security.
Users can enable 2FA in account settings and must verify with
authenticator app on subsequent logins.

Closes #123
```

```
fix(api): resolve race condition in order processing

Multiple concurrent requests were creating duplicate orders due to
non-atomic transaction handling. Added database-level locking to
ensure order creation is properly serialized.

Fixes #456
```

```
docs(readme): update installation instructions for Python 3.11
```

**Bad examples**:

```
❌ "fixed stuff"
   Problem: Too vague, no context

❌ "update code"
   Problem: Not specific, doesn't explain what or why

❌ "WIP: working on feature"
   Problem: WIP commits should be rebased before merging

❌ "Added new feature and fixed several bugs and updated docs"
   Problem: Multiple unrelated changes, should be separate commits
```

---

## Resources

### Detailed Type Guidelines

**feat** - New features or capabilities
- Adding a new API endpoint
- Implementing a new user-facing feature
- Adding support for a new data format
- Example: `feat(api): add bulk import endpoint for customer data`

**fix** - Bug fixes
- Resolving incorrect behavior
- Fixing crashes or errors
- Correcting data issues
- Example: `fix(validation): prevent negative values in quantity field`

**docs** - Documentation only
- README updates
- Code comments
- API documentation
- User guides
- Example: `docs(api): add examples for authentication endpoints`

**refactor** - Code restructuring
- Extracting functions or classes
- Renaming for clarity
- Reorganizing file structure
- No behavior changes
- Example: `refactor(services): extract common validation logic to utilities`

**test** - Test additions or updates
- Adding missing test coverage
- Updating tests for refactored code
- Fixing broken tests
- Example: `test(auth): add integration tests for 2FA flow`

**chore** - Maintenance tasks
- Dependency updates
- Build configuration
- Tooling changes
- Example: `chore(deps): update pandas to 2.0.0`

**perf** - Performance improvements
- Optimization changes
- Reducing memory usage
- Improving query performance
- Example: `perf(database): add index on user_id for faster lookups`

### Edge Cases

**Breaking changes**: Use `!` after type or `BREAKING CHANGE:` in footer
```
feat(api)!: change authentication endpoint to use OAuth2

BREAKING CHANGE: The /auth endpoint now requires OAuth2 tokens
instead of API keys. Update all clients to use the new flow.
```

**Merge commits**: Auto-generated, acceptable as-is
```
Merge pull request #123 from feature/new-auth
```

**Reverts**: Use `revert:` prefix
```
revert: feat(auth): add two-factor authentication support

This reverts commit abc123def456 due to production issues.
```

**Co-authors**: Add in footer
```
feat(analytics): add user behavior tracking

Co-authored-by: Jane Doe <jane@example.com>
Co-authored-by: John Smith <john@example.com>
```

### Integration with Tooling

**Git hooks**: Use pre-commit hooks to validate format
```bash
# .git/hooks/commit-msg
#!/bin/sh
commit_msg=$(cat "$1")
pattern="^(feat|fix|docs|refactor|test|chore|perf|style|ci)(\(.+\))?: .+"

if ! echo "$commit_msg" | grep -qE "$pattern"; then
  echo "Error: Commit message must follow Conventional Commits format"
  echo "Format: <type>(<scope>): <subject>"
  exit 1
fi
```

**Commit templates**: Configure Git to use a template
```bash
git config commit.template .gitmessage
```

`.gitmessage`:
```
# <type>(<scope>): <subject> (max 50 chars)
# |<----  Using a Maximum Of 50 Characters  ---->|

# Explain why this change is being made
# |<----   Try To Limit Each Line to a Maximum Of 72 Characters   ---->|

# Provide links or keys to any relevant tickets, articles or resources
# Example: Closes #23

# --- COMMIT END ---
# Type can be:
#    feat     (new feature)
#    fix      (bug fix)
#    refactor (code change without feature/fix)
#    docs     (documentation changes)
#    test     (adding/updating tests)
#    chore    (maintenance)
#    perf     (performance improvement)
#    style    (formatting, missing semicolons)
#    ci       (CI/CD changes)
# --------------------
# Remember:
#    - Use imperative mood ("add" not "added")
#    - Subject starts with lowercase
#    - No period at end of subject
#    - Separate subject from body with blank line
#    - Wrap body at 72 characters
# --------------------
```

### Personal Patterns

**Multi-repo changes**: Reference related commits
```
feat(shared): update data models for new customer schema

Related changes:
- api-service: abc123
- web-app: def456
```

**Research experiments**: Use `experiment` scope
```
feat(experiment): implement XGBoost model variant for A/B test
```

**Data pipeline changes**: Be specific about data impact
```
fix(pipeline): correct date parsing in customer import job

Previous logic incorrectly parsed ISO dates with timezone offsets,
causing records from 11pm-midnight UTC to be assigned wrong dates.
Affects ~500 records from 2024-01-15 to 2024-01-20.
```
