---
title: GitHub Workflow Patterns
description: branching strategies, merge practices, and GitHub collaboration patterns
tags: [github, workflow, branching, merging, collaboration, best-practices]
---

# GitHub Workflow Patterns

## Metadata

**Purpose**: Best practices for branching, merging, releases, and GitHub features
**Applies to**: All projects using GitHub
**Version**: 1.0.0

---

## Instructions

### Branch Naming Conventions

**Standard format**:
```
<type>/<short-description>
```

**Types**:
- `feature/` - New features
- `fix/` or `bugfix/` - Bug fixes
- `hotfix/` - Urgent production fixes
- `refactor/` - Code refactoring
- `docs/` - Documentation updates
- `experiment/` - Research experiments
- `chore/` - Maintenance tasks

**Examples**:
- ✅ `feature/add-customer-segmentation`
- ✅ `fix/resolve-auth-timeout`
- ✅ `hotfix/patch-security-vulnerability`
- ✅ `refactor/extract-validation-logic`
- ❌ `john-dev` (not descriptive)
- ❌ `temp-branch` (not meaningful)
- ❌ `FEATURE-123` (all caps, no description)

**Guidelines**:
- Use lowercase with hyphens
- Be descriptive but concise
- Include ticket number if applicable: `feature/PROJ-123-add-export`
- Avoid personal names or dates

### Merge Strategies

**Squash Merge** (recommended for most PRs)
- Combines all commits into single commit
- Clean, linear history
- Use when: Feature branch has messy commit history

```bash
# GitHub: "Squash and merge" button
# CLI:
git merge --squash feature/my-feature
git commit -m "feat: add new feature"
```

**Merge Commit** (preserve commit history)
- Keeps all individual commits
- Shows full development history
- Use when: Commits are clean and tell a story

```bash
# GitHub: "Create a merge commit" button
# CLI:
git merge --no-ff feature/my-feature
```

**Rebase** (update feature branch)
- Replay commits on top of target branch
- Linear history, no merge commits
- Use when: Updating feature branch with main

```bash
# Update feature branch with main
git checkout feature/my-feature
git rebase main
```

**Default**: Squash merge for cleaner history

### Pre-Commit Hook Requirements

**All projects should use pre-commit hooks for**:

1. **Code quality**:
   - Linting (ruff, eslint, etc.)
   - Formatting (black, prettier, etc.)
   - Type checking (mypy, typescript)

2. **Security**:
   - Secret detection (detect-secrets)
   - Dependency scanning

3. **Git hygiene**:
   - Commit message format validation
   - Prevent commits to main/master
   - Check for debugging code

**Setup**:
```bash
# Install pre-commit
pip install pre-commit

# Install hooks
pre-commit install

# .pre-commit-config.yaml example
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.5.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-added-large-files
      - id: check-merge-conflict

  - repo: https://github.com/psf/black
    rev: 23.12.1
    hooks:
      - id: black

  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.1.9
    hooks:
      - id: ruff
```

### Draft PRs

**Use draft PRs for**:
- Work in progress
- Seeking early architectural feedback
- CI/CD pipeline testing
- Demonstrating approach

**Workflow**:
```
1. Create PR as draft
2. Add [WIP] or [Draft] prefix to title (optional)
3. Request feedback in comments
4. Mark "Ready for review" when complete
```

**Draft PR checklist before marking ready**:
- [ ] All tests passing
- [ ] Code complete (no TODOs for this PR)
- [ ] Description updated
- [ ] Self-review completed

### GitHub Actions Integration Points

**Common automation use cases**:

1. **PR validation**:
   - Run tests on every PR
   - Check code coverage
   - Lint and format checks
   - Security scans

2. **Branch protection**:
   - Require status checks to pass
   - Require reviews before merge
   - Prevent force pushes to main
   - Require signed commits

3. **Automated workflows**:
   - Auto-label PRs based on files changed
   - Auto-assign reviewers
   - Post coverage reports
   - Deploy to staging environments

**Example workflow** (`.github/workflows/pr-checks.yml`):
```yaml
name: PR Checks

on:
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run tests
        run: pytest
      - name: Check coverage
        run: pytest --cov --cov-fail-under=80
```

### Protected Branches

**Main branch should be protected with**:
- Require PR before merging
- Require status checks to pass
- Require review from code owners
- Dismiss stale reviews on new commits
- Require linear history (optional)
- Prevent force pushes
- Prevent deletions

---

## Resources

### Complete Workflow Example

**Feature Development Workflow**:

```bash
# 1. Create and switch to feature branch
git checkout main && git pull origin main
git checkout -b feature/add-export-api

# 2. Make changes and commit
git add src/api/export.py
git commit -m "feat(api): add customer data export endpoint"

# 3. Push and create PR
git push -u origin feature/add-export-api
gh pr create --title "feat: add customer data export API" \
  --body "Adds endpoint for exporting customer data as CSV/JSON"

# 4. Address review feedback, merge via GitHub UI (squash merge)

# 5. Clean up local branch
git checkout main && git pull origin main
git branch -d feature/add-export-api
```

**For hotfixes**: Use `hotfix/` branch type, label as `security,hotfix`, request expedited review

**For rebasing**: `git fetch origin && git rebase origin/main && git push --force-with-lease`

### Conflict Resolution

```bash
git status  # Identify conflicted files
# Resolve conflicts in editor (look for <<<<<<<, =======, >>>>>>>)
git add <resolved-files>
git rebase --continue  # or git merge --continue
git push --force-with-lease
```

**Prevention**: Keep PRs small, merge main frequently, use feature flags

### Release Workflows

**SemVer** (`vMAJOR.MINOR.PATCH`): For libraries/APIs - MAJOR=breaking, MINOR=features, PATCH=fixes
**CalVer** (`vYYYY.MM.MICRO`): For applications/pipelines with time-based releases

**Release Process**:
```bash
git checkout -b release/v1.2.0
# Update version files and CHANGELOG.md
gh pr create --title "chore: release v1.2.0"
# After merge:
git checkout main && git pull origin main
git tag -a v1.2.0 -m "Release v1.2.0" && git push origin v1.2.0
gh release create v1.2.0 --title "Version 1.2.0" --notes "Release notes..."
```

### Personal Patterns

**Multi-Repo Changes**

When changes span multiple repositories:

```markdown
## Related PRs
This change requires updates across multiple repos:

- [ ] API Service: username/repo#123
- [ ] Web App: username/repo#456
- [ ] Data Pipeline: username/repo#789

**Merge order**: API → Pipeline → Web App
**Deployment**: Coordinate deployment window
```

**Research Experiments**

Use `experiment/` branches for exploratory work:

```bash
git checkout -b experiment/test-xgboost-model

# Document outcomes in PR description
# Merge if successful, close if unsuccessful
# Keep experiment history for reference
```

**Data Pipeline Branches**

Include data validation in PR workflow:

```bash
# 1. Create feature branch with data change
# 2. Run validation queries in staging
# 3. Document data impact in PR
# 4. Get data team review
# 5. Plan backfill if needed
# 6. Merge and monitor data quality
```

### Common Git Operations

| Issue | Solution |
|-------|----------|
| **Committed to wrong branch** | `git reset --soft HEAD~1 && git stash && git checkout correct-branch && git stash pop && git commit` |
| **Undo last commit (keep changes)** | `git reset --soft HEAD~1` |
| **Cherry-pick to another branch** | `git checkout target-branch && git cherry-pick <commit-hash>` |
| **Accidentally committed secrets** | Remove secret, commit, `git push --force-with-lease`, **rotate secret immediately** |

### GitHub Features to Leverage

**Code Owners** (`.github/CODEOWNERS`):
```
# Auto-assign reviewers based on files changed
*.py @data-team
src/api/* @backend-team
docs/* @documentation-team
```

**Issue Templates** (`.github/ISSUE_TEMPLATE/bug_report.md`):
```markdown
---
name: Bug Report
about: Report a bug
---

**Description**
Clear description of the bug

**Steps to Reproduce**
1. Step 1
2. Step 2

**Expected Behavior**
What should happen

**Actual Behavior**
What actually happened
```

**PR Templates** (`.github/pull_request_template.md`):
```markdown
## Purpose
Why is this change needed?

## Changes
- What was modified?

## Testing
- [ ] Tests added
- [ ] Manual testing completed

## Checklist
- [ ] Code follows style guidelines
- [ ] Documentation updated
```
