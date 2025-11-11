---
description: Run comprehensive pre-commit checks with project-aware validation
---

# Pre-Commit Check

You are running **pre-commit quality checks** before allowing a commit or push.

## Command Parameters

**Scope Parameter:**
- `--scope=commit` (default) - Check staged changes and commit message
- `--scope=push` - Check all commits on branch before push

**Auto-Fix Parameter:**
- `--auto-fix` (default: false) - Attempt to fix issues automatically

**Format Parameter:**
- `--format=console` (default) - Display results in console
- `--format=markdown` - Generate markdown report

**Output Parameter:**
- `--output=<path>` - Custom report path (only with --format=markdown)

**Usage Examples:**
```bash
/git-workflow:pre-commit-check                    # Check staged changes
/git-workflow:pre-commit-check --scope=push       # Check before push
/git-workflow:pre-commit-check --auto-fix         # Fix issues automatically
/git-workflow:pre-commit-check --format=markdown  # Generate report
```

## Objective

Run comprehensive quality checks based on:
1. Project type detection (Python, Data Science, Plugin Marketplace)
2. Pre-commit framework status (installed or not)
3. Universal checks (always run)
4. Project-specific checks (context-aware)

## Activated Agent

**Activate**: `git-workflow-specialist` agent

## Activated Skills

- **`commit-message-standards`** - Validate commit format
- **`github-workflow-patterns`** - Branch naming, pre-commit best practices
- **`pre-commit-quality-standards`** - Project type detection, quality checks, pre-commit configs

## Check Process

### Step 0: Check Git Status and Handle Unstaged Changes

**IMPORTANT**: Before running any checks, detect what files need to be checked.

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
If there are staged files, proceed to check them:
```
Found staged changes:
  - src/api/export.py
  - tests/test_export.py

Running quality checks on 2 staged files...
```

Continue to Step 1 (Detect Project Type).

#### State 2: No staged files, but unstaged/untracked files exist
If no files are staged but there are modified or new files, offer interactive options:

```
No staged changes found.

Detected modified/new files:
  - src/api/export.py (modified)
  - src/utils/validation.py (modified)
  - tests/test_export.py (new file)

What would you like to do?
1. ✓ Check all modified/new files (recommended)
2. ✏️  Stage specific files first, then check (git add -p)
3. ⏭️  Cancel - nothing to check
```

**If user chooses Option 1** (Check all files):
- Temporarily stage all modified/new files for checking purposes
- Run all quality checks
- After checks complete, **unstage** them if they weren't originally staged
- Report: "Files checked but not staged. Run /git-workflow:draft-commit to stage and commit."

**If user chooses Option 2** (Selective staging):
- Pause and instruct user to run `git add -p` or `git add <specific-files>`
- After staging, re-run pre-commit-check
- Continue to Step 1

**If user chooses Option 3** (Cancel):
- Exit with message: "No files to check. Make changes first."

#### State 3: No changes at all
If no staged, unstaged, or untracked files:
```
No changes detected.

Current state:
- Working directory clean
- No files staged for commit

Make some changes first, then run /git-workflow:pre-commit-check
```

Exit gracefully.

---

### Step 1: Detect Project Type

Use the **`pre-commit-quality-standards`** skill to detect project type(s).

Examine repository for indicators of:
- Python projects
- Data Science projects
- Plugin Marketplace projects
- Mixed projects (e.g., Python + Data Science)

### Step 2: Check Pre-Commit Status

```bash
# Check if pre-commit is configured
test -f .pre-commit-config.yaml && echo "configured" || echo "not configured"

# If configured, check if installed
pre-commit --version 2>/dev/null && echo "installed" || echo "not installed"
```

**Three scenarios**:
1. **Configured + Installed**: Run pre-commit hooks
2. **Configured but not installed**: Warn and suggest `pre-commit install`
3. **Not configured**: Run Claude-native checks + offer to generate config

### Step 3: Universal Checks (Always Run)

Run all universal checks from the **`pre-commit-quality-standards`** skill:

1. **Commit Message Validation** (if `--scope=commit`) - Use `commit-message-standards` skill
2. **Branch Naming Validation** - Use `github-workflow-patterns` skill
3. **Secret Detection** - Use patterns from `pre-commit-quality-standards`
4. **Large File Detection** - Thresholds defined in `pre-commit-quality-standards`
5. **Merge Conflict Markers** - Check for `<<<<<<<`, `=======`, `>>>>>>>`
6. **Trailing Whitespace** - Use `git diff --staged --check`
7. **Direct Commits to Protected Branches** - Fail if on main/master

### Step 4: Run Pre-Commit Hooks (If Configured)

If `.pre-commit-config.yaml` exists and pre-commit is installed:

```bash
# For commit scope - run on staged files only
pre-commit run

# For push scope - run on all files
pre-commit run --all-files
```

**Parse output**:
- Extract failed hooks
- Report specific file/line issues
- If `--auto-fix`: re-run with auto-fixing enabled

**If pre-commit configured but NOT installed**:
```markdown
⚠️ **Pre-commit configured but not installed**

Your project has `.pre-commit-config.yaml` but pre-commit is not installed.

To install:
\```bash
pip install pre-commit
pre-commit install
\```

Continuing with Claude-native checks...
```

### Step 5: Project-Specific Claude-Native Checks

If pre-commit is NOT configured, run project-specific checks from the **`pre-commit-quality-standards`** skill based on detected project type(s):

- **Python Projects**: Syntax validation, debug statements, print statements, hardcoded paths
- **Plugin Marketplace Projects**: JSON validation, markdown linting, plugin structure
- **Data Science Projects**: Notebook size, outputs in notebooks, large data files

See `pre-commit-quality-standards` skill for complete check definitions.

### Step 6: Generate Recommendations

If pre-commit is NOT configured, use the **`pre-commit-quality-standards`** skill to:
1. Select appropriate pre-commit config template based on detected project type
2. Offer to create `.pre-commit-config.yaml` file
3. Provide installation instructions

## Output Format

### When All Checks Pass

```markdown
## Pre-Commit Check Results

**Scope**: commit
**Project Type**: Python
**Pre-commit**: Configured ✅

---

**All Checks Passed** ✅

- ✅ Branch naming follows convention (feature/add-export)
- ✅ Not on protected branch
- ✅ No secrets detected
- ✅ No large files
- ✅ No merge conflict markers
- ✅ Pre-commit hooks passed (black, ruff, mypy)

**Checked Files**:
- src/api/export.py
- src/utils/validation.py
- tests/test_export.py

**Summary**: Quality checks passed! Files are ready to commit.

**Next Step**: Run /git-workflow:draft-commit to stage and commit these changes.
```

### When Checks Fail

```markdown
## Pre-Commit Check Results

**Scope**: commit
**Project Type**: Python
**Pre-commit**: Not configured ⚠️

---

**Status**: ❌ FAIL

**Blocking Issues**:

1. ❌ **Commit message invalid**
   - Current: "fix bug"
   - Problem: Too vague, missing scope
   - Fix: Use format `fix(<scope>): specific description`
   - Run: `/git-workflow:draft-commit` to generate proper message

2. ❌ **Potential secret detected**
   - File: `src/config.py`
   - Line 15: `api_key = "sk-1234567890abcdef"`
   - Action: Remove hardcoded secret, use environment variable

3. ❌ **Debug statement found**
   - File: `src/api/users.py`
   - Line 42: `import pdb; pdb.set_trace()`
   - Action: Remove debug statement

**Warnings**:

1. ⚠️ **Large file staged**
   - File: `data/export.csv` (15.2 MB)
   - Consider: Use Git LFS or exclude from repository

2. ⚠️ **Print statements found**
   - File: `src/api/export.py`
   - Lines: 23, 45, 67
   - Consider: Use logging instead of print()

**Summary**: 3 errors, 2 warnings - Cannot commit

---

## Recommendations

**Install pre-commit hooks** for automated checking:

\```bash
pip install pre-commit
\```

Create `.pre-commit-config.yaml` using the template from **`pre-commit-quality-standards`** skill for your project type:
- Python projects: Use Python template (black, ruff, mypy, detect-secrets)
- Plugin Marketplace: Use Marketplace template (markdownlint, YAML/JSON validation)
- Data Science: Use Data Science template (nbQA, nbstripout, black, ruff)

Then run:
\```bash
pre-commit install
\```

Would you like me to create this file for you? (yes/no)
```

### When Pre-Commit Configured But Not Installed

```markdown
## Pre-Commit Check Results

**Scope**: commit
**Project Type**: Python
**Pre-commit**: Configured but not installed ⚠️

---

⚠️ **Pre-commit hooks are configured but not installed**

Your project has `.pre-commit-config.yaml` with these hooks:
- black (formatting)
- ruff (linting)
- mypy (type checking)
- detect-secrets

**To install**:
\```bash
pip install pre-commit
pre-commit install
\```

**Continuing with Claude-native checks...**

---

[Rest of check results...]
```

## Auto-Fix Workflow

When `--auto-fix` is enabled:

### Step 1: Attempt Automatic Fixes

**If pre-commit configured**:
```bash
# Many pre-commit hooks support auto-fixing
pre-commit run --all-files
```

Hooks like black, prettier, trailing-whitespace will fix issues automatically.

**If using Claude-native checks**:
- Fix trailing whitespace
- Remove debug statements (if user confirms)
- Format basic syntax issues

### Step 2: Report What Was Fixed

```markdown
## Auto-Fix Results

**Fixes Applied** ✅:

1. ✅ **Formatted code with black**
   - Files: `src/api/users.py`, `src/api/export.py`
   - Changes: Line length normalized, imports sorted

2. ✅ **Removed trailing whitespace**
   - Files: 5 files affected

**Issues Requiring Manual Fix** ❌:

1. ❌ **Potential secret detected**
   - File: `src/config.py`
   - Cannot auto-fix: Requires manual review and environment variable setup

2. ❌ **Commit message invalid**
   - Run: `/git-workflow:draft-commit` to generate proper message

**Next Steps**:
1. Review auto-applied fixes: `git diff`
2. Fix remaining issues manually
3. Re-run checks: `/git-workflow:pre-commit-check`
```

## Push-Scope Checks

When `--scope=push`:

### Additional Checks:

1. **Validate All Commits on Branch**:
```bash
# Get all commits on current branch
git log main..HEAD --format="%H %s"

# Validate each commit message
for commit in $(git log main..HEAD --format="%H"); do
  git log -1 $commit --format="%s%n%n%b" | validate
done
```

2. **Check for Divergence**:
```bash
# Check if branch is behind main
git fetch origin
git rev-list HEAD..origin/main --count
```
⚠️ **Warn** if branch is behind main (suggest rebase/merge)

3. **Verify No Direct Commits to Main**:
Already covered in universal checks, but more critical for push.

4. **Check for Force Push Protection**:
```bash
# Check if this would be a force push
git push --dry-run --force 2>&1 | grep "rejected"
```
❌ **Fail** if force push to protected branch

## Important Notes

- **Non-blocking by default**: Checks report issues but don't prevent commits (user decides)
- **Can be integrated**: Results can drive actual git hooks via exit codes
- **Progressive enhancement**: Works without pre-commit, better with it
- **Project-aware**: Adapts checks to project type
- **Educational**: Explains WHY issues are problems and HOW to fix

**Exit codes** (for git hook integration):
- `0` - All checks passed
- `1` - Blocking issues found
- `2` - Warnings only (non-blocking)

---

**Remember**: This command is flexible - it works standalone, as a pre-commit hook, or as a quality gate before pushing.
