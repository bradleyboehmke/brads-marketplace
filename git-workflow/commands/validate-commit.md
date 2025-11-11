---
description: Validate commit message quality against standards
---

# Validate Commit Message

You are validating a **commit message** against standards.

## Command Parameters

**Message Parameter:**
- `--message="commit message"` - Message to validate (default: read from git staging)

**Format Parameter:**
- `--format=console` (default) - Display validation results in console
- `--format=markdown` - Generate markdown validation report

**Output Parameter:**
- `--output=<path>` - Custom report path (only with --format=markdown)

**Usage Examples:**
```bash
/git-workflow:validate-commit                                    # Validate staged commit
/git-workflow:validate-commit --message="fix bug in auth"        # Validate specific message
/git-workflow:validate-commit --format=markdown                  # Generate report
```

## Objective

Validate commit message against:
1. Conventional Commits format
2. commit message standards
3. Issue linking policy
4. Quality criteria

## Activated Agent

**Activate**: `git-workflow-specialist` agent

## Activated Skills

- **`commit-message-standards`** - Format, quality, issue linking policy

## Validation Process

### Step 1: Get Commit Message

If `--message` provided: Use that
If not: Read from git prepare-commit-msg or last commit

### Step 2: Check Format

✅ **Pass criteria:**
- Matches: `<type>(<scope>): <subject>`
- Type is valid (feat, fix, docs, refactor, test, chore, perf, style, ci)
- Subject ≤50 characters
- Uses imperative mood
- Starts with lowercase
- No period at end

❌ **Fail if:**
- No type prefix
- Invalid type
- Subject too long
- Vague (e.g., "fix bug", "update code")

### Step 3: Check Issue Linking

Based on commit type:
- **feat, fix**: Issue reference REQUIRED
- **refactor, perf**: Issue reference RECOMMENDED
- **docs, chore, test, style**: Issue reference OPTIONAL

✅ **Pass**: Has `Closes #123`, `Fixes #456`, or `Relates to #789`
⚠️ **Warning**: Missing but recommended
❌ **Fail**: Missing and required

### Step 4: Check Quality

- Not WIP/temp language
- Specific (not vague)
- Clear intent
- Appropriate body for non-trivial changes

## Output Format

```markdown
## Validation Results

**Message:**
\```
fix bug in auth
\```

**Status:** ❌ FAIL

**Issues Found:**

1. ❌ **Missing commit type format**
   - Current: "fix bug in auth"
   - Required: `fix(<scope>): <subject>`
   - Fix: Add type prefix and scope

2. ❌ **Subject too vague**
   - "bug in auth" doesn't explain what was fixed
   - Be specific: which bug? what behavior?

3. ❌ **Missing issue reference**
   - fix commits require issue reference
   - Add: `Fixes #<issue-number>`

**Correct Example:**
\```
fix(auth): resolve session timeout on mobile devices

Fixes #456
\```

**Summary:** 3 errors, 0 warnings

---

**Next Steps:**

Would you like me to:
1. 🤖 **Run `/git-workflow:draft-commit`** - Generate a proper message automatically
2. ✏️ **Help you fix this message** - Guide you through corrections
3. ❌ **Cancel** - Just show validation results

Enter your choice (1, 2, or 3):
```

## Pass Example

```markdown
## Validation Results

**Message:**
\```
feat(api): add customer export endpoint

Adds new /api/customers/export endpoint supporting CSV and JSON formats.

Closes #234
\```

**Status:** ✅ PASS

**Checks:**
- ✅ Conventional Commits format
- ✅ Valid type: feat
- ✅ Clear, specific subject (38 characters)
- ✅ Imperative mood
- ✅ Issue reference present (required for feat)
- ✅ Body provides context

**Summary:** All checks passed

✅ This message is ready to commit!
```

## Important Notes

- **Agent use**: Can be called by git-workflow-specialist when user provides a commit message
- **CI/CD ready**: Can run in pipelines to enforce standards
- **Pre-commit hook**: Can block bad commits
- **Learning tool**: Shows WHY a message is wrong

## Interactive Failure Handling

When validation **FAILS**, prompt user with next steps:

**Option 1 - Run draft-commit**:
```markdown
Running `/git-workflow:draft-commit` to generate a proper message...
[Executes draft-commit command]
```

**Option 2 - Help fix message**:
```markdown
Let's fix your message step by step:

**Current:** "fix bug in auth"

**Step 1: Add commit type**
Your message starts with "fix" which is good, but needs proper format.
\```
fix(<scope>): <subject>
\```

**Step 2: Add scope**
What component is affected? (e.g., auth, api, ui)
[Wait for user input: "auth"]

**Step 3: Make subject specific**
Current: "bug in auth"
What specific bug? What behavior was wrong?
[Wait for user input: "session timeout on mobile"]

**Step 4: Add issue reference**
fix commits require an issue reference. What issue does this fix?
[Wait for user input: "456"]

**Updated message:**
\```
fix(auth): resolve session timeout on mobile

Fixes #456
\```

Would you like to commit with this message? (yes/no)
```

**Option 3 - Cancel**:
```markdown
Validation results saved. No further action taken.
```

## When Validation Passes

If message passes all checks, simply confirm:
```markdown
✅ Message validated successfully - ready to commit!
```

No need to prompt for further action.

---

**Remember**:
- Validation failures → Offer to help fix or regenerate
- Validation passes → Confirm and done
- Can be used standalone or by git-workflow-specialist agent
