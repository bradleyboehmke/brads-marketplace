---
description: Generate standards-compliant commit message and handle staging workflow
---

# Draft Commit Message

You are helping a developer create a **standards-compliant commit message** for their changes.

This command intelligently handles staging: if files aren't staged yet, it offers to stage them before drafting the commit message.

## Command Parameters

This command supports the following optional parameters:

**Type Parameter:**
- `--type=feat|fix|docs|refactor|test|chore|perf|style|ci` - Commit type (optional, inferred if not provided)

**Scope Parameter:**
- `--scope=<scope>` - Commit scope/component (optional, e.g., `auth`, `api`, `ui`)

**Format Parameter:**
- `--format=console` (default) - Display draft message and prompt for action

**Interactive Parameter:**
- `--interactive` (default: true) - Prompt user to accept/edit/cancel after drafting
- `--interactive=false` - Just display draft without prompting

**Usage Examples:**
```bash
/git-workflow:draft-commit                           # Auto-detect, interactive prompt
/git-workflow:draft-commit --type=feat               # Specify type, interactive
/git-workflow:draft-commit --type=fix --scope=auth   # Specify type and scope
/git-workflow:draft-commit --interactive=false       # Just show draft, no prompt
```

## Objective

Generate a high-quality commit message that:
1. Follows Conventional Commits format
2. Meets commit message standards
3. Includes appropriate issue reference if needed
4. Provides clear context and rationale

## Activated Agent

**Activate**: `git-workflow-specialist` agent

## Activated Skills

The agent will activate:
- **`commit-message-standards`** - Conventional Commits format, quality criteria, issue linking policy

## Process

Follow this workflow to draft the commit message:

### Step 0: Check Git Status and Handle Staging

**IMPORTANT**: Before drafting the commit message, ensure files are staged.

```bash
# Check for staged changes
git diff --cached --name-only

# Check for unstaged changes
git diff --name-only

# Check for untracked files
git ls-files --others --exclude-standard
```

**Determine the state**:

#### State 1: Files already staged
If there are staged files, proceed directly to Step 1 (Analyze Staged Changes).

```
Found staged changes:
  - src/api/export.py
  - tests/test_export.py

Analyzing changes for commit message...
```

#### State 2: No staged files, but modified/new files exist
If no files are staged but there are modified or new files, offer interactive staging:

```
No staged changes found.

Detected modified/new files:
  - src/api/export.py (modified)
  - src/utils/validation.py (modified)
  - tests/test_export.py (new file)

⚠️ Note: Pre-commit checks should be run before committing.
Last pre-commit-check: [timestamp if available, or "Not run yet"]

What would you like to do?
1. ✓ Stage all files and continue (recommended if checks passed)
2. ✏️  Select specific files to stage (git add -p)
3. ⚠️  Run /git-workflow:pre-commit-check first
4. ❌ Cancel - don't commit yet
```

**If user chooses Option 1** (Stage all):
```bash
# Stage all modified and new files
git add -A

# Confirm staging
✓ Staged 3 files

# Continue to Step 1 (Analyze Staged Changes)
```

**If user chooses Option 2** (Selective staging):
- Prompt user: "Which files would you like to stage?"
- User provides list or pattern
- Stage those specific files
- If they want to use `git add -p`: pause and let them do it manually, then re-run draft-commit

```bash
# User specifies: src/api/export.py, tests/test_export.py
git add src/api/export.py tests/test_export.py

✓ Staged 2 files:
  - src/api/export.py
  - tests/test_export.py

Excluded from staging:
  - src/utils/validation.py

# Continue to Step 1
```

**If user chooses Option 3** (Run pre-commit-check first):
- Exit with message: "Run /git-workflow:pre-commit-check to validate quality first, then come back to draft-commit."
- This is the recommended workflow if checks haven't been run

**If user chooses Option 4** (Cancel):
- Exit with message: "No changes staged. Stage your changes when ready."

#### State 3: No changes at all
If no staged, unstaged, or untracked files:

```
❌ **No Changes to Commit**

Current state:
- Working directory clean
- No files staged for commit
- No modified or new files

Make some changes first, then run /git-workflow:draft-commit
```

Exit gracefully.

---

### Step 1: Analyze Staged Changes

After files are staged (either already staged or staged via Step 0):

```bash
# Get staged changes
git diff --staged
```

Examine:
- Which files are changed
- What functionality is affected
- Scope/component of changes
- Nature of the changes (new feature, bug fix, etc.)

### Step 2: Determine Commit Type

If `--type` not provided, infer from changes:
- **feat**: New functionality, new files with features
- **fix**: Bug fixes, error handling improvements
- **docs**: Documentation-only changes (README, comments)
- **refactor**: Code restructuring without behavior change
- **test**: Test additions or updates
- **chore**: Dependency updates, build config, tooling
- **perf**: Performance improvements
- **style**: Formatting, whitespace, code style
- **ci**: CI/CD configuration changes

### Step 3: Determine Scope

If `--scope` not provided, infer from files:
- Look at directory structure (e.g., `src/auth/*` → scope: `auth`)
- Look at module names (e.g., `api/users.py` → scope: `api` or `users`)
- If changes span multiple areas, choose the primary one or omit scope

Common scopes in general:
- `auth`, `api`, `ui`, `database`, `pipeline`, `models`, `tests`, `docs`, `config`

### Step 4: Activate Agent and Skill

```
Activate: git-workflow-specialist agent
Agent activates: commit-message-standards skill
```

### Step 5: Craft Commit Message

**Subject line** (≤50 characters):
```
<type>(<scope>): <clear, specific description>
```

Requirements:
- Use imperative mood ("add" not "added")
- Start with lowercase
- No period at end
- Be specific about what changed

**Body** (optional but recommended):
- Explain WHY the change was made
- Provide context or background
- Note any important technical decisions
- Wrap lines at 72 characters

**Footer** (for issue references):
- Check commit type against issue linking policy
- If feat or fix: Include issue reference (REQUIRED)
- If refactor/perf: Include issue reference (RECOMMENDED)
- If docs/chore/test: Issue reference optional

Format:
- `Closes #123` - For features that close an issue
- `Fixes #456` - For bug fixes
- `Relates to #789` - For related work

### Step 6: Check Against Standards

Validate the draft message:
- [ ] Follows Conventional Commits format
- [ ] Subject ≤50 characters
- [ ] Uses imperative mood
- [ ] Specific and clear (not vague like "fix bug")
- [ ] Includes issue reference if required by type
- [ ] Body provides context (if non-trivial change)
- [ ] No WIP or temp language

### Step 7: Present Draft Message

Display the complete draft message in a code block:

```
<type>(<scope>): <subject>

[Body explaining why and providing context]

[Footer with issue reference if applicable]
```

Then provide:
1. **Explanation** of why this message structure was chosen
2. **Issue linking note** if issue reference is required but missing
3. **Alternative suggestions** if applicable

## Output Format

Present the draft commit message like this:

```markdown
## Draft Commit Message

\```
feat(auth): add two-factor authentication support

Implements TOTP-based 2FA for user accounts to enhance security.
Users can enable 2FA in account settings and must verify with
authenticator app on subsequent logins.

Closes #123
\```

## Explanation

**Type**: `feat` - This adds new functionality (2FA feature)
**Scope**: `auth` - Changes are in authentication system
**Subject**: Clear and specific about what was added
**Body**: Explains the implementation approach and user impact
**Footer**: Includes `Closes #123` as required for feat commits

## Notes

✅ Follows Conventional Commits format
✅ Subject is 48 characters (under 50 limit)
✅ Uses imperative mood ("add")
✅ Includes required issue reference for feat type
✅ Body provides clear context

## Next Steps

**If `--interactive=true` (default)**, prompt the user:

\```markdown
Would you like to:
1. ✅ **Accept and commit** - Use this message and execute `git commit`
2. ✏️  **Edit message** - Modify the message before committing
3. ❌ **Cancel** - Don't commit, just show the draft

Enter your choice (1, 2, or 3):
\```

**Option 1: Accept and commit**
- Execute the commit with the drafted message
- Show confirmation: "✅ Committed successfully with message: [first line]"

**Option 2: Edit message**
- Display the message in an editable format
- User can modify subject, body, or footer
- After editing, prompt again: Accept edited version or Cancel
- Execute commit with edited message

**Option 3: Cancel**
- Display: "Draft message saved for reference but not committed."
- Provide copy command:
  \```bash
  git commit -m "$(cat <<'EOF'
  feat(auth): add two-factor authentication support

  Implements TOTP-based 2FA for user accounts to enhance security.
  Users can enable 2FA in account settings and must verify with
  authenticator app on subsequent logins.

  Closes #123
  EOF
  )"
  \```

**If `--interactive=false`**, just display the draft and copy command without prompting.
```

## Special Cases

**No Issue Exists**:
If feat/fix commit but no issue reference found in changes:
```markdown
⚠️ **Issue Reference Required**

This is a `feat` commit, which requires an issue reference per standards.

Options:
1. Create a GitHub issue first, then update commit message
2. Provide detailed context in commit body explaining why no issue

Example with detailed context:
\```
feat(api): add rate limiting to prevent abuse

Implements token bucket algorithm with 100 requests/minute limit.
Prevents API abuse and ensures fair usage across all clients.

No issue created as this is a quick security hardening measure
responding to recent spike in automated requests.
\```
```

**Multiple Changes in Staging**:
If staged changes mix multiple types (feat + fix):
```markdown
⚠️ **Multiple Change Types Detected**

Your staged changes include both new features AND bug fixes.

Recommendation: Split into separate commits for cleaner history.

Suggested approach:
1. Unstage all: `git reset`
2. Stage and commit feature changes first
3. Then stage and commit bug fixes separately
```

**Trivial Changes** (docs, formatting):
```markdown
## Draft Commit Message (Simple)

\```
docs(readme): update installation instructions for Python 3.11
\```

This is a simple documentation change, so no body or issue reference needed.
```

## Important Notes

- **Read staged changes first**: Always examine `git diff --staged` before drafting
- **Be specific**: Avoid vague subjects like "update code" or "fix bug"
- **Context matters**: Provide body for non-trivial changes
- **Issue linking**: Enforce policy from commit-message-standards skill
- **No assumptions**: If unclear, ask user for clarification
- **Quality over speed**: Take time to craft a good message

## Error Handling

| Error | Message | Resolution |
|-------|---------|------------|
| **No changes** | ❌ No staged/unstaged changes to commit | Make changes first, then run command |
| **Ambiguous type** | Commit type unclear from changes | Specify: `/git-workflow:draft-commit --type=feat` |

## Interactive Workflow (Default)

When `--interactive=true` (default), follow this flow:

1. **Draft message** (as described above)
2. **Present to user** with explanation and validation notes
3. **Prompt for action**:
   ```
   Would you like to:
   1. ✅ Accept and commit
   2. ✏️  Edit message
   3. ❌ Cancel
   ```

4. **Handle user choice**:

   **Choice 1 - Accept and commit**:
   ```bash
   # Execute commit
   git commit -m "$(cat <<'EOF'
   [drafted message]
   EOF
   )"

   # Confirm
   ✅ Committed successfully: feat(auth): add two-factor authentication support
   ```

   **Choice 2 - Edit message**:
   ```markdown
   ## Edit Commit Message

   Current draft:
   \```
   feat(auth): add two-factor authentication support

   Implements TOTP-based 2FA for user accounts to enhance security.
   Users can enable 2FA in account settings and must verify with
   authenticator app on subsequent logins.

   Closes #123
   \```

   Please provide your edited version below:
   [Wait for user input]

   [After user provides edited version]

   Updated message:
   \```
   [user's edited version]
   \```

   Would you like to:
   1. ✅ Commit with edited message
   2. ❌ Cancel
   ```

   **Choice 3 - Cancel**:
   ```markdown
   Draft message not committed. You can manually commit using:

   \```bash
   git commit -m "$(cat <<'EOF'
   [drafted message]
   EOF
   )"
   \```
   ```

---

**Remember**: Interactive mode (default) allows executing commits directly. Non-interactive mode just displays the draft.
