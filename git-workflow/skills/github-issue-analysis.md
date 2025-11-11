---
title: GitHub Issue Analysis
description: Scoring rubrics and clustering methodology for analyzing GitHub issues
tags: [github, issues, scoring, clustering, analysis]
---

# GitHub Issue Analysis

## Metadata

**Purpose**: Analyze GitHub issues with multi-dimensional scoring and clustering
**Applies to**: Repository investigation and issue backlog analysis
**Version**: 1.0.0

---

## Instructions

### Issue Scoring Dimensions

Score each issue on a scale of 1-5 (low to high) across four dimensions:

#### 1. Risk Score (1-5)
Assess the potential negative impact if the issue is NOT addressed:

- **5 - Critical Risk**: Security vulnerability, data loss, production outage, compliance violation
- **4 - High Risk**: Major feature broken, significant performance degradation, user-blocking bug
- **3 - Medium Risk**: Moderate bug affecting some users, technical debt that will compound
- **2 - Low Risk**: Minor bug with workarounds, cosmetic issue, edge case problem
- **1 - Minimal Risk**: Nice-to-have improvement, suggestion, question

**Detection patterns**:
- Keywords: `security`, `vulnerability`, `crash`, `data loss`, `broken`, `urgent`, `blocker`
- Labels: `security`, `critical`, `bug`, `p0`, `blocker`
- Issue state: Open for >90 days with high comment activity

#### 2. Value Score (1-5)
Assess the positive impact if the issue IS addressed:

- **5 - Transformative**: Major feature enabling new use cases, significant UX improvement
- **4 - High Value**: Important enhancement improving core workflows, performance boost
- **3 - Medium Value**: Useful improvement benefiting many users, code quality enhancement
- **2 - Low Value**: Minor convenience, small optimization, documentation improvement
- **1 - Minimal Value**: Cosmetic change, personal preference, duplicate effort

**Detection patterns**:
- Keywords: `feature`, `enhancement`, `improve`, `optimize`, `speed up`, `user request`
- Labels: `enhancement`, `feature`, `performance`, `ux`
- Community engagement: High thumbs-up reactions, many comments requesting feature

#### 3. Ease Score (1-5)
Assess the effort required to implement (inverse scale - 5 is easiest):

- **5 - Trivial**: Documentation update, config change, simple one-liner fix
- **4 - Easy**: Small bug fix, minor refactor, straightforward enhancement (<1 day)
- **3 - Moderate**: Feature addition requiring new code, moderate refactor (1-3 days)
- **2 - Challenging**: Complex feature, architectural change, multiple dependencies (1-2 weeks)
- **1 - Very Hard**: Major refactor, breaking changes, requires research/prototyping (>2 weeks)

**Detection patterns**:
- Keywords: `easy`, `good first issue`, `help wanted`, `typo`, `documentation`
- Labels: `good-first-issue`, `easy`, `documentation`, `beginner-friendly`
- Code references: Issues with specific file/line references are often easier

#### 4. DocQuality Score (1-5)
Assess how well the issue is documented:

- **5 - Excellent**: Clear description, reproduction steps, expected behavior, context, examples
- **4 - Good**: Clear problem statement, some context, actionable
- **3 - Adequate**: Basic description, understandable but missing details
- **2 - Poor**: Vague description, missing context, requires clarification
- **1 - Very Poor**: Unclear, no details, cannot action without extensive follow-up

**Detection patterns**:
- Length: Longer issues (>500 chars) often have better documentation
- Structure: Issues with headers, code blocks, numbered steps
- Completeness: Includes version info, environment details, error messages

### Issue Clustering and Themes

Group related issues by detecting common themes:

#### Theme Detection Approach

1. **Keyword extraction**: Extract significant terms from title and body
2. **Label analysis**: Group by common labels
3. **Component detection**: Identify affected components/modules
4. **Similarity scoring**: Find issues with overlapping keywords

#### Common Theme Categories

- **Bug Clusters**: Similar error messages, same component, related failures
- **Feature Requests**: Related enhancements, common user needs
- **Performance Issues**: Speed, memory, scalability concerns
- **Documentation**: Missing docs, unclear guides, examples needed
- **Dependencies**: Third-party library issues, version conflicts
- **DevOps/Infrastructure**: CI/CD, deployment, build issues
- **Security**: Vulnerabilities, auth, permissions

#### Clustering Algorithm

```
For each issue:
  1. Extract keywords from title and body (remove stopwords)
  2. Extract labels
  3. Count keyword overlaps with other issues
  4. If overlap > threshold (e.g., 3+ keywords), mark as related
  5. Group related issues into clusters
  6. Name cluster by most common keywords
```

### Staleness Detection

**Definition**: Issues with no activity for ≥N days (default: 60)

**Activity indicators**:
- New comments
- Label changes
- Status updates
- Commits referencing the issue

**Staleness categories**:
- **Fresh**: Activity within last 30 days
- **Aging**: 30-60 days since last activity
- **Stale**: 60-90 days since last activity
- **Very Stale**: 90+ days since last activity

**Action recommendations**:
- **Very Stale**: Consider closing with explanation or ping assignees
- **Stale**: Review priority, add to backlog grooming
- **Aging**: Monitor for staleness
- **Fresh**: Active work, no action needed

### Issue Bucketing

Categorize issues into actionable buckets based on scores:

1. **High Value**: Value ≥ 4, Risk ≥ 3 → Priority work
2. **High Risk**: Risk ≥ 4 → Address urgently regardless of value
3. **Newcomer Friendly**: Ease ≥ 4, DocQuality ≥ 3 → Good first issues
4. **Automation Candidate**: Ease ≥ 4 AND at least 2 similar issues detected by clustering → Consider scripting/automation
5. **Needs Context**: DocQuality ≤ 2 → Request more information
6. **Stale**: No activity ≥ stale_days → Consider closing/archiving

---

## Resources

### Scoring Examples

#### Example 1: Security Vulnerability
```
Title: "SQL injection in login endpoint"
Risk: 5 (critical security issue)
Value: 5 (must fix)
Ease: 3 (moderate fix, requires testing)
DocQuality: 5 (clear reproduction steps, example payload)
Bucket: High Risk
```

#### Example 2: Documentation Typo
```
Title: "Fix typo in README.md - 'installtion' -> 'installation'"
Risk: 1 (minimal impact)
Value: 1 (minor improvement)
Ease: 5 (trivial one-character change)
DocQuality: 5 (exact location specified)
Bucket: Newcomer Friendly
```

#### Example 3: Feature Request
```
Title: "Add dark mode support"
Risk: 1 (no negative impact if not done)
Value: 4 (highly requested UX improvement)
Ease: 2 (significant UI/CSS work)
DocQuality: 3 (clear request but missing design specs)
Bucket: High Value
```

#### Example 4: Vague Bug Report
```
Title: "App doesn't work"
Risk: ? (unclear)
Value: ? (unclear)
Ease: ? (cannot assess)
DocQuality: 1 (no details whatsoever)
Bucket: Needs Context
```

### CLI Integration

The analysis uses GitHub CLI (`gh`) for read-only access:

```bash
# Fetch all open issues
gh issue list --state open --limit 1000 --json number,title,body,labels,createdAt,updatedAt,comments

# Fetch issues with specific labels
gh issue list --label bug --state open --json number,title,body,labels,createdAt,updatedAt

# Fetch issues since specific date
gh issue list --state all --search "updated:>2024-01-01"
```

### Output Format

**Console Output**: Structured dashboard with tables and buckets
**Markdown Output**: Detailed report with scores, themes, and recommendations

Example markdown structure:
```markdown
# GitHub Issue Analysis

## Summary
- Total issues analyzed: 47
- Stale issues: 12
- High risk issues: 3
- High value issues: 8

## Issue Buckets

### High Risk (3 issues)
- #42: SQL injection vulnerability [Risk:5, Value:5, Ease:3]
- #38: Data corruption in export [Risk:5, Value:4, Ease:2]

### High Value (8 issues)
...

## Themes
1. **Performance** (5 issues): #12, #23, #34, #45, #56
2. **Documentation** (8 issues): ...

## Stale Issues
- #15: Last activity 87 days ago
- #22: Last activity 92 days ago
```
