---
title: Pull Request Quality Standards
description: PR sizing, scope, documentation, and review-readiness criteria
tags: [github, pull-requests, standards, code-review, collaboration]
---

# Pull Request Quality Standards

## Metadata

**Purpose**: Define what makes a good PR at (size, focus, documentation)
**Applies to**: All pull requests in projects
**Version**: 1.0.0

---

## Instructions

### Single-Purpose Principle

**Each PR should do ONE thing well**

A PR should represent a single, cohesive change:
- One feature
- One bug fix
- One refactoring
- One set of related documentation updates

**❌ Multi-purpose PRs** (avoid these):
- Feature + unrelated bug fixes
- Refactoring + new functionality
- Multiple independent features
- Bug fixes + dependency updates + docs

**Why it matters**:
- Easier to review and understand
- Clearer rollback if issues arise
- Better Git history for debugging
- Faster review cycles

### PR Size Guidelines

**Target sizes** (lines of code changed):
- **Small**: < 200 LOC ✅ (ideal, ~1-2 hours review time)
- **Medium**: 200-500 LOC ⚠️ (acceptable, ~2-4 hours review time)
- **Large**: 500-1000 LOC ⚠️ (needs justification, ~1 day review time)
- **Too Large**: > 1000 LOC ❌ (should be split)

**File count**: Aim for < 15 files changed

**Exceptions** (large PRs acceptable when):
- Generated code (migrations, API clients)
- Vendored dependencies
- Large data files or configuration
- Initial project setup
- Bulk renaming/reformatting (use separate PR)

**When PR is too large**, split by:
- Logical components (backend → frontend)
- Sequential steps (refactor → feature → tests)
- Module/service boundaries
- Infrastructure vs application changes

### Title Format

**Use clear, descriptive titles**:

```
<type>: <clear description of change>
```

**Examples**:
- ✅ `feat: add customer segmentation API endpoint`
- ✅ `fix: resolve race condition in order processing`
- ✅ `refactor: extract validation logic to shared utilities`
- ❌ `updates` (too vague)
- ❌ `fix bug` (which bug?)
- ❌ `Feature/123` (not descriptive)

**Title should**:
- Start with lowercase (after type)
- Use imperative mood
- Be specific about what changed
- Avoid ticket numbers only (include description)

### Description Requirements

**Minimum requirements** for all PRs:

1. **Purpose**: Why is this change needed?
2. **Changes**: What was modified (high-level)?
3. **Testing**: How was this tested?
4. **Impact**: What's affected by this change?
5. **Issue Reference**: Link to related GitHub issue(s)

### Issue Linking Policy for PRs

**Issue references are REQUIRED for**:
- Feature PRs (new functionality)
- Bug fix PRs (resolving issues)
- Breaking change PRs
- Large refactorings (> 200 LOC)

**Issue references are RECOMMENDED for**:
- Performance improvements
- Smaller refactorings
- Significant test additions

**Issue references are OPTIONAL for**:
- Documentation-only updates
- Dependency updates (chores)
- Minor formatting/style fixes

**Format in PR description**:
- `Closes #123` - Closes an issue when PR merges
- `Fixes #456` - Fixes a bug (auto-closes issue)
- `Resolves #789` - Resolves an issue
- `Relates to #101` - Related but doesn't auto-close
- `Part of #102` - Part of larger epic/feature
- Multiple issues: `Closes #123, #456`

**Placement**: Include in Purpose section or at end of description

**Examples**:
```markdown
## Purpose
Add email validation to prevent registration with invalid addresses.

Closes #234
```

```markdown
## Purpose
Fix session timeout issue reported by multiple mobile users.

This addresses the root cause identified in investigation.

Fixes #456
```

**Template**:

```markdown
## Purpose
Brief explanation of why this change is needed.

## Changes
- High-level summary of what was modified
- Key technical decisions
- Any breaking changes

## Testing
- [ ] Unit tests added/updated
- [ ] Integration tests pass
- [ ] Manual testing completed
- [ ] Tested on [environment/platform]

## Screenshots (if UI changes)
[Add screenshots or recordings]

## Impact
- Who/what is affected?
- Any performance implications?
- Dependencies or follow-up work?

## Checklist
- [ ] Code follows style guidelines
- [ ] Tests added for new functionality
- [ ] Documentation updated
- [ ] No debugging code or console logs
```

### Multi-Purpose PR Detection

**Red flags** indicating a multi-purpose PR:

🚩 **Multiple unrelated file groups**:
```
Changes:
- src/auth/*           (authentication changes)
- src/reports/*        (reporting feature)
- src/database/*       (schema updates)
```
→ Split into 3 PRs

🚩 **Commit history with mixed types**:
```
feat: add new dashboard
fix: resolve login issue
chore: update dependencies
docs: update README
```
→ Each should be separate PR

🚩 **Description uses "and" repeatedly**:
```
"This PR adds user authentication AND fixes the bug in reports
AND updates dependencies AND refactors the API"
```
→ Split into 4 PRs

🚩 **Changes span multiple services/repos**:
→ Consider separate PRs per service, or use stack of dependent PRs

### Draft PRs

Use draft PRs for:
- Work in progress (WIP)
- Seeking early feedback
- Sharing approach before completion
- Long-running feature branches

**Mark as draft when**:
- Tests aren't passing
- Code isn't ready for review
- Exploring an approach

**Convert to ready when**:
- All tests pass
- Code is complete
- Ready for full review

---

## Resources

### Size Refactoring Strategies

**Strategy 1: Layer-based splitting**
```
PR 1: Database schema changes
PR 2: Backend API implementation
PR 3: Frontend integration
PR 4: Tests and documentation
```

**Strategy 2: Feature-based splitting**
```
PR 1: Core feature (minimal viable)
PR 2: Additional options/configuration
PR 3: UI polish and edge cases
PR 4: Performance optimizations
```

**Strategy 3: Refactor-then-feature**
```
PR 1: Refactor existing code (no behavior change)
PR 2: Add new feature using refactored structure
```

**Strategy 4: Component isolation**
```
PR 1: Shared utilities (used by feature)
PR 2: Service A changes
PR 3: Service B changes
PR 4: Integration and tests
```

### Good PR Examples

**Example 1: Small, focused feature**
```
Title: feat: add email validation to user registration

Description:
## Purpose
Users were able to register with invalid email addresses, causing
delivery failures for password reset emails.

## Changes
- Added regex-based email validation in registration form
- Added backend validation in user creation endpoint
- Display user-friendly error for invalid emails

## Testing
- [x] Unit tests for validation logic
- [x] Integration tests for registration flow
- [x] Manual testing with various email formats

## Impact
- Affects new user registration only
- Existing users unaffected
- No database changes required

Files changed: 4 (+120, -15)
```

**Example 2: Well-scoped refactor**
```
Title: refactor: extract common validation logic to utilities

Description:
## Purpose
Validation logic was duplicated across 8 API endpoints, making
updates error-prone and inconsistent.

## Changes
- Created validation utilities module
- Extracted email, phone, date validation to shared functions
- Updated 8 endpoints to use shared validators
- No behavior changes (existing tests still pass)

## Testing
- [x] All existing unit tests pass unchanged
- [x] Added tests for new validation utilities
- [x] Manual regression testing on auth flows

## Impact
- All API endpoints using validation
- Easier to add new validation rules in future
- No user-facing changes

Files changed: 12 (+250, -180)
```

### PR Review Checklist

**For PR authors (self-review)**:
- [ ] Single, focused purpose
- [ ] Reasonable size (< 500 LOC if possible)
- [ ] Clear title and description
- [ ] All tests passing
- [ ] No commented-out code
- [ ] No console.log / debugging statements
- [ ] Documentation updated
- [ ] Breaking changes clearly marked
- [ ] Follow-up issues created for future work

**For reviewers**:
- [ ] Purpose is clear and justified
- [ ] Changes match description
- [ ] No scope creep or unrelated changes
- [ ] Code follows standards
- [ ] Tests are adequate
- [ ] No security issues
- [ ] Performance impact acceptable
- [ ] Documentation sufficient

### Breaking Change Communication

**If PR includes breaking changes**:

1. **Mark clearly in title**:
   ```
   feat!: change authentication to OAuth2
   ```

2. **Add BREAKING CHANGE section**:
   ```markdown
   ## BREAKING CHANGE

   The `/auth` endpoint now requires OAuth2 tokens instead of API keys.

   **Migration guide**:
   1. Register OAuth2 application
   2. Update client to obtain tokens
   3. Replace API key header with Bearer token

   **Timeline**: Old authentication deprecated 2024-06-01, removed 2024-09-01
   ```

3. **Communicate to stakeholders**:
   - Tag affected teams in PR
   - Post in relevant Slack channels
   - Update migration documentation

### Personal Patterns

**Research PRs**: Include experiment context
```markdown
## Research Context
- **Hypothesis**: XGBoost will improve prediction accuracy by 5%
- **Baseline**: Current model (Random Forest, 0.82 AUC)
- **Metrics**: AUC, precision, recall on validation set
- **Outcome**: Document results in PR comments
```

**Data pipeline PRs**: Include data impact
```markdown
## Data Impact
- **Affected tables**: customer_data, transactions
- **Estimated runtime**: +15 minutes per run
- **Backfill needed**: Yes, for records since 2024-01-01
- **Validation queries**: [link to SQL validation]
```

**Multi-repo PRs**: Link related PRs
```markdown
## Related PRs
- API service: #123
- Web app: #456
- Data pipeline: #789

**Merge order**: API → Pipeline → Web App
```

### Handling Large PRs (When Unavoidable)

If you must create a large PR:

1. **Provide detailed description** with section breakdown
2. **Add inline comments** explaining complex sections
3. **Create review guide**:
   ```markdown
   ## Review Guide

   Recommended review order:
   1. Start with `src/models/*.py` (core logic)
   2. Then `src/api/*.py` (API changes)
   3. Then `tests/*` (test coverage)
   4. Finally `docs/*` (documentation)

   Focus areas:
   - Data validation logic in `validators.py`
   - Performance of batch processing in `processor.py`
   ```
4. **Break into logical commits** that can be reviewed individually
5. **Offer to pair review** for complex sections
