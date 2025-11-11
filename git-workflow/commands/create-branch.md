---
description: Interactive guidance for creating properly named Git branches following conventions
---

# Create Branch Command

You are helping a developer create a new Git branch following Personal naming conventions and workflow best practices.

## Objective

Provide **interactive, suggestive guidance** for branch creation that:
1. Analyzes current Git state
2. Suggests a properly formatted branch name
3. Gives the user control to accept, modify, or skip
4. Educates on conventions without blocking workflow

## Workflow

### Step 1: Analyze Current State

Check the current Git state:

```bash
# Current branch and status
git branch --show-current
git status

# Check if on main and if it's up-to-date
git fetch origin
git status
```

Identify:
- **Current branch**: What branch is the user on?
- **Uncommitted changes**: Are there staged or unstaged changes?
- **Base branch status**: Is main (or intended base) up-to-date with remote?

### Step 2: Generate Branch Name Suggestion

**Activate the `github-workflow-patterns` skill** to reference branch naming conventions.

Based on user's request, infer:
- **Branch type**: feature, fix, bugfix, hotfix, refactor, docs, experiment, chore
- **Description**: Short, kebab-case description of the work
- **Ticket number** (if mentioned): e.g., PROJ-123

**Format**: `<type>/<description>` or `<type>/<ticket>-<description>`

**Examples**:
- User says "add customer export feature" → `feature/add-customer-export`
- User says "fix auth timeout bug" → `fix/resolve-auth-timeout`
- User says "fix JIRA-456 data validation" → `fix/JIRA-456-data-validation`
- User says "refactor validation logic" → `refactor/extract-validation-logic`
- User says "urgent production fix" → `hotfix/patch-critical-error`

**Rules**:
- Use lowercase with hyphens (kebab-case)
- Be descriptive but concise (3-5 words)
- Avoid personal names, dates, or generic terms like "temp" or "dev"

### Step 3: Determine Base Branch

**Default**: Branch off `main` (or `master`)

**Special cases**:
- If user is on a feature branch and mentions "sub-feature" or related work → suggest branching from current
- If user explicitly says "from <branch>" → use that branch
- For hotfixes → always suggest `main` (or production branch)

### Step 4: Present Interactive Suggestion

Format your response as a clear, actionable suggestion with 3-4 options:

```
Based on your request, I suggest:

Current branch: <current-branch> [status indicators]
Branch off from: <base-branch> [status]
Suggested name: <type>/<description>

[Show rationale if helpful - e.g., "This follows convention: <type>/<short-description>"]

What would you like to do?
1. ✓ Create branch '<suggested-name>'
2. ✏️  Modify the branch name
3. ⏭️  Skip - continue working in current branch
[4. Additional option if relevant - see Special Cases below]
```

**Status indicators**:
- `(clean, up-to-date ✓)` - Clean state, synced with remote
- `(uncommitted changes ⚠️)` - Has uncommitted work
- `(behind origin ⚠️)` - Needs to pull latest
- `(feature branch)` - Currently on a feature branch

### Step 5: Handle User Response

**Option 1: Accept suggestion**
- User says: "yes", "1", "create it", "go ahead", "looks good"
- Action: Execute branch creation

```bash
# If base branch needs updating
git checkout <base-branch>
git pull origin <base-branch>

# Create and switch to new branch
git checkout -b <suggested-name>

# Optionally set up remote tracking (if pushing immediately)
git push -u origin <suggested-name>
```

- Confirm:
```
✓ Created and switched to: <branch-name>

Next steps:
1. Make your changes
2. Run /git-workflow:pre-commit-check to validate quality
3. Run /git-workflow:draft-commit to create commit
4. Run /git-workflow:draft-pr to create pull request
```

**Option 2: Modify branch name**
- User says: "call it <new-name>", "2", "use <new-name> instead", "change to <new-name>"
- Action: Parse new name, validate it follows conventions, create with modified name
- If name doesn't follow conventions, warn but allow (user choice)

```
✓ Created and switched to: <user-modified-name>

Note: This name doesn't follow standard convention (<type>/<description>).
Consider using: <suggested-alternative> for future branches.

Next steps:
1. Make your changes
2. Run /git-workflow:pre-commit-check to validate quality
3. Run /git-workflow:draft-commit to create commit
4. Run /git-workflow:draft-pr to create pull request
```

**Option 3: Skip**
- User says: "no", "3", "skip", "not now", "continue on current branch"
- Action: Do nothing, acknowledge

```
Understood. Continuing work on current branch: <current-branch>

Remember: You can run /git-workflow:create-branch anytime to create a properly named branch.
```

## Special Cases

### Case 1: Uncommitted Changes

If user has uncommitted changes, add a 4th option:

```
⚠️  Warning: You have uncommitted changes in current branch (<current-branch>)

Suggested name: <type>/<description>
Branch off from: <base-branch>

What would you like to do?
1. ✓ Stash changes, create branch, restore changes
2. ✏️  Modify the branch name
3. ⏭️  Skip - continue working in current branch
4. 💾 Commit changes first (run pre-commit-check → draft-commit)
```

**If user chooses Option 1** (stash):
```bash
git stash push -m "WIP: stashing for branch <new-branch>"
git checkout <base-branch>
git pull origin <base-branch>
git checkout -b <new-branch>
git stash pop
```

**If user chooses Option 4** (commit first):
- Switch to pre-commit-check workflow first
- Then draft-commit workflow
- After commit completes, return to branch creation suggestion

### Case 2: Currently on Feature Branch

If user is on a feature branch (not main/master):

```
Current branch: <feature-branch> (feature branch)
Suggested name: <type>/<description>
Branch off from: <feature-branch>

Note: Creating a sub-feature branch from your current branch.
If you want to start fresh from main instead, choose option 4.

What would you like to do?
1. ✓ Create branch '<suggested-name>' from current branch
2. ✏️  Modify the branch name
3. ⏭️  Skip - continue working in current branch
4. 🔄 Branch from main instead
```

**If user chooses Option 4**:
```bash
git checkout main
git pull origin main
git checkout -b <suggested-name>
```

### Case 3: Base Branch Behind Remote

If main (or base) is behind remote:

```
⚠️  Note: <base-branch> is behind origin/<base-branch>

Suggested name: <type>/<description>
Branch off from: <base-branch> (will pull latest first)

What would you like to do?
1. ✓ Pull latest <base-branch>, then create branch '<suggested-name>'
2. ✏️  Modify the branch name
3. ⏭️  Skip - continue working in current branch
```

### Case 4: Already on Target Branch

If a branch with the suggested name already exists:

```
⚠️  Branch '<suggested-name>' already exists

What would you like to do?
1. 🔄 Switch to existing branch '<suggested-name>'
2. ✏️  Use a different name (e.g., '<suggested-name>-v2')
3. ⏭️  Skip - continue working in current branch
```

## Parameters

This command accepts optional parameters (usually inferred by the agent):

- `--type=<type>` - Branch type (feature, fix, hotfix, refactor, docs, experiment, chore)
- `--description=<desc>` - Brief description of the work
- `--from=<branch>` - Base branch to branch from (default: auto-detect, usually main)
- `--ticket=<number>` - Optional ticket/issue number to include in branch name

**Example invocations**:
```bash
# Agent infers from user's natural language request
User: "Create a branch to add customer export"
Agent: /git-workflow:create-branch --type=feature --description="add customer export"

# Explicit invocation with parameters
/git-workflow:create-branch --type=fix --description="resolve auth timeout" --ticket=PROJ-123

# Minimal invocation (will prompt for details)
/git-workflow:create-branch
```

## Output Format

Always use **console format** (interactive only - markdown reports don't apply here).

Present information in a clear, scannable format:
- Use **emoji sparingly** for status indicators (✓, ⚠️, ✏️, ⏭️, 💾, 🔄)
- Use **numbered options** for user choices
- Show **concrete commands** when executing actions
- Provide **clear next steps** after completion

## Key Principles

1. **Suggestive, not prescriptive**: Offer guidance but give users control
2. **Educational**: Explain conventions so users learn, not just follow
3. **Context-aware**: Adapt to current Git state and user situation
4. **Non-blocking**: Never prevent users from proceeding if they choose to skip
5. **Integrated**: Flow naturally into draft-commit and draft-pr workflows

## Example Interaction

**User**: "Let's start working on adding a customer segmentation feature"

**Command Response**:
```
Based on your request, I suggest:

Current branch: main (clean, up-to-date ✓)
Branch off from: main
Suggested name: feature/add-customer-segmentation

This follows convention: <type>/<short-description>

What would you like to do?
1. ✓ Create branch 'feature/add-customer-segmentation'
2. ✏️  Modify the branch name
3. ⏭️  Skip - continue working in current branch
```

**User**: "1"

**Command Response**:
```
✓ Created and switched to: feature/add-customer-segmentation

Next steps:
1. Make your changes
2. Run /git-workflow:pre-commit-check to validate quality
3. Run /git-workflow:draft-commit to create commit
4. Run /git-workflow:draft-pr to create pull request
```

---

**Remember**: This command is about empowering developers with best practices while respecting their autonomy and workflow preferences.
