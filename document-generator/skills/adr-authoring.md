---
title: ADR Authoring
description: MADR format structure and best practices for Architecture Decision Records
tags: [adr, documentation, decisions, madr]
---

# ADR Authoring

## Metadata

**Purpose**: Provide MADR template structure and ADR best practices
**Version**: 1.0.0

---

## ADR Template

```markdown
# ADR-XXX: [Short Decision Title]

**Status:** [Proposed/Accepted/Superseded/Rejected]
**Date:** YYYY-MM-DD
**Deciders:** [Names or roles]
**Maturity Level:** [Experimental/Prototype/Production]
**Handoff Impact:** [None/Low/Medium/High]

## Context

[What is the issue we're addressing? What stage of the project are we in?
What business problem or research question drives this decision?]

## Decision Drivers

- [Driver 1: e.g., Must achieve 95% accuracy for business case]
- [Driver 2: e.g., Inference latency must be <100ms]
- [Driver 3: e.g., Solution must be interpretable for business users]
- [Driver 4: e.g., Limited to X budget/compute resources]

## Options Considered

### Option 1: [Name]
**Description:** [Brief explanation]

**Pros:**
- [Advantage 1]
- [Advantage 2]

**Cons:**
- [Disadvantage 1]
- [Disadvantage 2]

**Evaluation Results:** [Benchmark numbers, if applicable]

### Option 2: [Name] ⭐ SELECTED
**Description:** [Brief explanation]

**Pros:**
- [Advantage 1]
- [Advantage 2]

**Cons:**
- [Disadvantage 1]
- [Disadvantage 2]

**Evaluation Results:** [Benchmark numbers, if applicable]

## Decision

We will [clear, active voice statement of what we're doing].

[For production decisions] This will be handed off to [team name] with the following support: [describe transition plan].

## Consequences

### Positive Outcomes
- [What becomes easier or better]
- [Capabilities we gain]

### Negative Outcomes
- [What becomes harder]
- [Capabilities we sacrifice]

### Risks & Mitigation
- **Risk:** [Potential problem]
  **Mitigation:** [How we'll address it]

### Implications for Business Team *(if applicable)*
- **What they need to know:** [Critical context for maintenance]
- **What they can modify:** [Safe changes they can make independently]
- **What requires re-engagement:** [Changes that need our team's input]
- **Required expertise:** [Skills needed to maintain this]

## Related ADRs

- Supersedes: [ADR-XXX if replacing an older decision]
- Related to: [ADR-YYY if connected to other decisions]
- Informed by: [ADR-ZZZ if building on previous work]

## References

[Links to detailed documentation, code, experiments, papers, etc.]
```

## Naming and Numbering

**Filename format**: `XXX-title-in-kebab-case.md`
**Sequential numbering**: 001, 002, 003, etc.
**Storage location**: `adr/` directory (Personal standard)

**IMPORTANT**:
- All ADRs MUST be stored in `adr/` directory
- If the `adr/` directory does not exist, create it first: `mkdir -p adr`
- Do NOT store ADRs in `docs/adr/` or any other location

## Maturity Levels

**Experimental** (Tier 1):
- Algorithm selection, feature engineering, evaluation metrics
- Review: Author + 1 peer (1-2 days)

**Prototype** (Tier 2):
- Infrastructure choices, in-market test design, data pipelines
- Review: Author + technical lead + 1 developer (3-5 days)

**Production** (Tier 3):
- Production architecture, monitoring, retraining strategies
- Review: Author + technical lead + business rep (5-7 days with meeting)

## Handoff Impact Levels

- **None**: Internal research decision, no handoff
- **Low**: Minor impact on business team maintenance
- **Medium**: Requires business team understanding
- **High**: Critical for business team success, requires training

## Status Lifecycle

1. **Proposed** - Under review, not yet accepted
2. **Accepted** - Approved and active
3. **Rejected** - Considered but not chosen
4. **Superseded** - Replaced by a newer ADR (reference the new ADR number)

## Best Practices

**Title**:
- Describes the decision, not the problem
- Noun phrase (e.g., "Use of PostgreSQL for feature store")

**Context**:
- What problem are we solving?
- What constraints exist?
- Why does this matter?

**Decision Drivers**:
- List 3-5 key factors influencing the decision
- Be specific (e.g., "Team has PostgreSQL expertise")

**Considered Options**:
- Always include at least 2-3 alternatives
- Show you explored options

**Consequences**:
- Be honest about trade-offs
- List both positive and negative impacts
- Include neutral consequences too

**Links**:
- Reference related ADRs
- Link to external documentation
- Show decision relationships

## When to Write ADRs

**Always write for**:
- Core methodology choices (algorithms, model architecture)
- Data architecture (storage, pipelines, schemas)
- Infrastructure decisions (cloud, framework, deployment)
- Evaluation approach changes
- Decisions persisting to production
- Significant pivots
- Failed experiments (status: Rejected)

**Use judgment for**:
- Temporary workarounds (if marked non-permanent)
- Tool choices for exploration (if not affecting deliverables)
- Hyperparameter decisions (unless novel or critical)

**Don't write for**:
- Individual experiment runs
- Personal workflow preferences
- Notebook organization
- Obvious/trivial choices

**Rule of thumb**: If someone might ask "why did we do it this way?" 6 months from now, write an ADR.
