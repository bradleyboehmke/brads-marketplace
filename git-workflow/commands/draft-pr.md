---
description: Generate standards-compliant PR title and description from branch changes
---

# Draft PR Description

You are helping a developer create a **standards-compliant pull request** for their branch.

## Command Parameters

**Base Branch Parameter:**
- `--base=main` - Base branch for comparison (default: main)

**Interactive Parameter:**
- `--interactive` (default: true) - Prompt to create PR after drafting
- `--interactive=false` - Just show draft without creating PR

**Format Parameter:**
- `--format=console` (default) - Display draft and prompt for action

**Usage Examples:**
```bash
/git-workflow:draft-pr                        # Compare to main, interactive
/git-workflow:draft-pr --base=develop         # Compare to develop branch
/git-workflow:draft-pr --interactive=false    # Just show draft
```

## Objective

Generate a high-quality PR that:
1. Follows PR quality standards
2. Has clear, descriptive title
3. Includes complete description (Purpose, Changes, Testing, Impact)
4. References appropriate GitHub issue(s)
5. Flags if PR is too large

## Activated Agent

**Activate**: `git-workflow-specialist` agent

## Activated Skills

- **`pr-quality-standards`** - PR sizing, scope, documentation, issue linking
- **`github-workflow-patterns`** - Best practices for PRs

## Process

### Step 1: Analyze Branch Changes

```bash
# Get commits on this branch
git log main..HEAD

# Get diff summary
git diff main...HEAD --stat

# Get full diff for analysis
git diff main...HEAD
```

Examine:
- Number of commits
- Files changed and LOC
- Scope of changes (single feature vs multiple)
- Component/module affected

### Step 2: Determine PR Title

Format: `<type>: <clear description>`

Type based on changes:
- `feat`: New functionality
- `fix`: Bug fixes
- `refactor`: Code restructuring
- `docs`: Documentation updates
- `chore`: Maintenance, dependencies

Example: `feat: add customer export API endpoint`

### Step 3: Check PR Size

**Size thresholds:**
- Small: < 200 LOC ✅
- Medium: 200-500 LOC ⚠️
- Large: 500-1000 LOC ⚠️ (flag and suggest split)
- Too Large: > 1000 LOC ❌ (recommend splitting)

**File count:** Flag if > 15 files

### Step 4: Detect Multi-Purpose Issues

Red flags:
- Commits with different types (feat + fix + chore)
- Changes in unrelated components
- Multiple features in one PR

If detected: Recommend splitting into focused PRs

### Step 5: Draft Description

**Template:**
```markdown
## Purpose
[Why is this change needed? What problem does it solve?]

## Changes
- [High-level summary of modifications]
- [Key technical decisions]
- [Any breaking changes]

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests pass
- [ ] Manual testing completed

## Impact
- [Who/what is affected?]
- [Performance implications?]
- [Follow-up work needed?]

[Issue reference: Closes #123]
```

### Step 6: Check Issue Linking

Based on PR type:
- **feat, fix, breaking**: Issue reference REQUIRED
- **refactor (>200 LOC), perf**: Issue reference RECOMMENDED
- **docs, chore, small refactor**: Issue reference OPTIONAL

Format: `Closes #123`, `Fixes #456`, `Relates to #789`

### Step 7: Present Draft

Show:
1. PR title
2. Complete description
3. Size analysis
4. Multi-purpose warnings (if any)
5. Issue linking status

## Output Format

```markdown
## Draft Pull Request

**Title:**
\```
feat: add customer export API endpoint
\```

**Description:**
\```markdown
## Purpose
Enable customers to export their data in CSV or JSON format for compliance
and data portability requirements.

## Changes
- Added /api/customers/export endpoint with format parameter
- Implemented CSV and JSON serializers
- Added authentication and rate limiting
- Updated API documentation

## Testing
- [x] Unit tests for serializers and endpoint
- [x] Integration tests for auth and rate limiting
- [x] Manual testing with sample customer data
- [x] Tested both CSV and JSON formats

## Impact
- New API endpoint available to all authenticated users
- Rate limited to 10 requests/hour per user
- No changes to existing endpoints

Closes #234
\```

---

## Size Analysis

**Files changed:** 8 files (+245, -12)
**LOC changed:** 257 lines
**Size:** Medium ⚠️ (within acceptable range)

✅ PR is reasonably sized and focused

---

## Validation

✅ Single-purpose PR (one feature)
✅ Clear title and description
✅ Issue reference present (required for feat)
✅ Testing section complete
✅ Impact documented

---

## Next Steps

**If `--interactive=true` (default)**, prompt:

Would you like to:
1. ✅ **Create PR** - Open pull request with this content
2. ✏️ **Edit** - Modify title or description
3. ❌ **Cancel** - Just show draft

Enter your choice (1, 2, or 3):
```

## Interactive Options

**Option 1 - Create PR:**
```bash
gh pr create \
  --title "feat: add customer export API endpoint" \
  --body "$(cat <<'EOF'
[full description]
EOF
)"

✅ Pull request created: #456
View at: https://github.com/owner/repo/pull/456
```

**Option 2 - Edit:**
```markdown
## Edit PR Content

Current title:
feat: add customer export API endpoint

New title (press Enter to keep current):
[Wait for user input]

Current description:
[Show description]

New description (press Enter to keep current):
[Wait for user input]

[After edits] Would you like to:
1. Create PR with edited content
2. Cancel
```

**Option 3 - Cancel:**
```markdown
Draft PR saved for reference. You can create it manually:

\```bash
gh pr create --title "feat: add customer export API endpoint" --body "..."
\```
```

## Size Warnings

**If PR is too large (>1000 LOC):**
```markdown
⚠️ **PR Too Large**

This PR changes 1,245 lines across 23 files, which will be difficult to review.

**Recommendation:** Split into smaller PRs

**Suggested split strategy:**
1. PR 1: Database schema changes (backend foundation)
2. PR 2: API endpoint implementation
3. PR 3: Frontend integration
4. PR 4: Tests and documentation

Would you like help planning the split? (yes/no)
```

**If multi-purpose detected:**
```markdown
⚠️ **Multi-Purpose PR Detected**

This PR includes changes for multiple unrelated purposes:
- New feature: customer export
- Bug fix: authentication timeout
- Chore: dependency updates

**Recommendation:** Create separate PRs for each purpose

1. feat: add customer export endpoint
2. fix: resolve authentication timeout
3. chore: update dependencies

This will make review easier and history clearer.

Would you like me to help split this? (yes/no)
```

## Important Notes

- **Analyze commits**: Look at all commits on branch, not just latest
- **Check for focus**: Flag if changes span unrelated components
- **Size matters**: Warn if too large for effective review
- **Issue linking**: Enforce based on PR type
- **Breaking changes**: Detect and highlight prominently

---

**Remember**: This generates PR drafts. For validating existing PRs, use `/git-workflow:validate-pr`.
