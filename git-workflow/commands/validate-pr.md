---
description: Validate PR quality and readiness against standards
---

# Validate Pull Request

You are validating a **pull request** against quality standards.

## Command Parameters

**PR Parameter:**
- `--pr=<number>` - PR number to validate (default: auto-detect from current branch)

**Repository Parameter:**
- `--repo=<owner/repo>` - Repository (default: auto-detect)

**Check Parameters:**
- `--check-size` (default: true) - Flag oversized PRs
- `--check-scope` (default: true) - Detect multi-purpose PRs

**Format Parameter:**
- `--format=console` (default) - Display validation in console
- `--format=markdown` - Generate markdown report

**Output Parameter:**
- `--output=<path>` - Custom report path (only with --format=markdown)

**Usage Examples:**
```bash
/git-workflow:validate-pr                     # Auto-detect PR from branch
/git-workflow:validate-pr --pr=123            # Validate specific PR
/git-workflow:validate-pr --format=markdown   # Generate report
```

## Objective

Validate PR against:
1. Title format and clarity
2. Description completeness
3. Size appropriateness
4. Single-purpose principle
5. Issue linking policy
6. Review readiness

## Activated Agent

**Activate**: `git-workflow-specialist` agent

## Activated Skills

- **`pr-quality-standards`** - Sizing, scope, documentation, issue linking
- **`github-workflow-patterns`** - PR best practices

## Validation Process

### Step 1: Fetch PR Details

```bash
gh pr view <number> --json title,body,files,additions,deletions,commits
```

### Step 2: Validate Title

✅ **Pass criteria:**
- Follows format: `<type>: <description>`
- Type is valid (feat, fix, refactor, docs, chore)
- Clear and specific (not vague)
- Descriptive (not just issue number)

❌ **Fail if:**
- No type prefix
- Vague (e.g., "updates", "changes")
- Only ticket number

### Step 3: Validate Description

✅ **Pass criteria:**
- Has Purpose section
- Has Changes summary
- Has Testing section
- Has Impact section
- Includes issue reference (if required by type)

❌ **Fail if:**
- Missing required sections
- No issue reference when required
- Empty or placeholder text

### Step 4: Check Size

**Thresholds:**
- Small: <200 LOC ✅
- Medium: 200-500 LOC ⚠️ (acceptable)
- Large: 500-1000 LOC ⚠️ (warning)
- Too Large: >1000 LOC ❌ (fail, recommend split)

**File count:** Warn if >15 files

### Step 5: Check Single-Purpose

Analyze commits and files for:
- Mixed commit types (feat + fix + chore)
- Unrelated file groups
- Multiple independent features

❌ **Fail if:** Multi-purpose detected

### Step 6: Check Issue Linking

Based on PR type:
- **feat, fix, breaking**: REQUIRED
- **refactor (>200 LOC), perf**: RECOMMENDED
- **docs, chore**: OPTIONAL

## Output Format

### Validation Failure

```markdown
## PR Validation Results

**PR:** #123 - "Updates to authentication"
**Status:** ❌ FAIL

---

**Issues Found:**

1. ❌ **Title not descriptive**
   - Current: "Updates to authentication"
   - Problem: Too vague, doesn't explain what was updated
   - Fix: `feat: add two-factor authentication support`

2. ❌ **Missing issue reference**
   - This appears to be a feature PR (feat)
   - Issue reference is REQUIRED for feat PRs
   - Add: `Closes #456` to description

3. ⚠️ **PR size warning**
   - Files changed: 18 files
   - LOC changed: 645 lines
   - Size: Large (consider splitting for easier review)

4. ❌ **Incomplete description**
   - Missing Testing section
   - Missing Impact section
   - Add these sections to meet standards

**Summary:** 3 errors, 1 warning

---

## Next Steps

Would you like me to:
1. 🤖 **Run `/git-workflow:draft-pr`** - Regenerate PR content from branch
2. ✏️ **Help you fix this PR** - Guide through corrections
3. ❌ **Cancel** - Just show validation results

Enter your choice (1, 2, or 3):
```

### Validation Success

```markdown
## PR Validation Results

**PR:** #234 - "feat: add customer export API endpoint"
**Status:** ✅ PASS

---

**Checks:**
- ✅ Title follows format (feat: ...)
- ✅ Clear and descriptive title
- ✅ Complete description (Purpose, Changes, Testing, Impact)
- ✅ Issue reference present (Closes #234)
- ✅ Reasonable size (257 LOC, 8 files)
- ✅ Single-purpose PR (focused on one feature)
- ✅ Testing documented

**Size Analysis:**
- Files changed: 8
- Lines added: 245
- Lines deleted: 12
- Total: 257 LOC (Medium, acceptable)

**Summary:** All checks passed - ready for review!
```

## Interactive Fix Workflow

**Option 1 - Regenerate with draft-pr:**
```markdown
Running `/git-workflow:draft-pr` to generate proper PR content...
[Executes draft-pr command on current branch]
```

**Option 2 - Help fix PR:**
```markdown
Let's fix your PR step by step:

**Issue 1: Title**
Current: "Updates to authentication"

What type of change is this?
- feat (new functionality)
- fix (bug fix)
- refactor (code restructuring)

[Wait for input: "feat"]

What specific feature was added?
[Wait for input: "two-factor authentication support"]

Updated title: `feat: add two-factor authentication support`

---

**Issue 2: Missing sections**
Your description needs:
- Testing section
- Impact section

What testing was performed?
[Wait for input, then add to description]

What's the impact of this change?
[Wait for input, then add to description]

---

**Issue 3: Issue reference**
feat PRs require an issue reference. What issue does this close?
[Wait for input: "456"]

Adding to description: `Closes #456`

---

**Updated PR:**
Title: feat: add two-factor authentication support
Description: [updated with fixes]

Would you like to update the PR? (yes/no)
```

**Option 3 - Cancel:**
```markdown
Validation results saved. No changes made to PR.
```

## Special Validations

**Breaking Changes:**
If PR title has `!` or description has `BREAKING CHANGE`:
```markdown
⚠️ **Breaking Change Detected**

This PR includes breaking changes.

Requirements for breaking change PRs:
- [ ] BREAKING CHANGE section in description
- [ ] Migration guide provided
- [ ] Timeline for deprecation (if applicable)
- [ ] Affected stakeholders tagged

[Check each requirement and report missing ones]
```

**Large PR Recommendations:**
```markdown
⚠️ **Large PR - Consider Splitting**

This PR changes 1,234 lines across 25 files.

**Suggested split strategy:**
1. Backend schema/API changes
2. Frontend integration
3. Tests and documentation

Smaller PRs are easier to review and less risky to merge.

Would you like help planning the split? (yes/no)
```

## Important Notes

- **Fetch live data**: Always get current PR state with `gh pr view`
- **Check all aspects**: Title, description, size, scope, issue linking
- **Be specific**: Point to exact issues with examples
- **Offer solutions**: Don't just flag problems, help fix them
- **Can run in CI**: Suitable for automated PR validation

---

**Remember**: This validates existing PRs. For creating PRs, use `/git-workflow:draft-pr`.
