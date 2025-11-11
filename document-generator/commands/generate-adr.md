---
description: Create an Architecture Decision Record (ADR) following MADR format
---

# Generate ADR

## Activated Agent

**Activate**: `adr-author` agent

The agent will help create a structured ADR document.

## Objective

Create an Architecture Decision Record (ADR) that documents an architectural decision with context, alternatives, and consequences following the MADR (Markdown Any Decision Record) format.

## Prerequisites

This command requires the **repo-investigator** plugin to be installed for codebase analysis capabilities.

If you haven't installed it yet:
```bash
claude plugin install repo-investigator@brads-marketplace
```

## Activated Skills

The agent will activate these skills:

1. **`adr-authoring`** (document-generator) - MADR template and ADR best practices
2. **`repository-analysis-methods`** (repo-investigator) - Understanding project architecture for context

## Process

**Before starting**, verify the repo-investigator plugin is available:

1. Check if `repo-investigator` skills are accessible
2. If `repository-analysis-methods` skill is not available:
   - Display a clear message to the user:
     ```
     ⚠️  Missing Dependency: repo-investigator plugin

     The generate-adr command requires the repo-investigator plugin for codebase analysis.

     Please install it:
       claude plugin install repo-investigator@brads-marketplace

     Then re-run this command.
     ```
   - Stop execution and wait for user to install the plugin

The agent will:

1. **Choose Workflow** - Ask user to select their preferred approach:
   - **Guided Interview**: Step-by-step questions with interactive clarification
   - **Comprehensive Input**: Provide all information at once

### Guided Interview Workflow

If user selects guided interview, ask questions one at a time or in small groups:

1. What architectural decision needs to be documented?
2. When was this decision made?
3. What problem does it solve?
4. What alternatives were considered?
5. What is the current status?
6. What are the consequences (positive and negative)?

### Comprehensive Input Workflow

If user selects comprehensive input, present this summary of required information:

```
Please provide the following information about your architectural decision:

**Required:**
- Decision title and brief description
- Problem/context that prompted this decision
- Chosen solution/approach

**Recommended:**
- Date of decision (defaults to today if not provided)
- Alternatives that were considered and why they were rejected
- Positive consequences/benefits
- Negative consequences/trade-offs
- Decision drivers (key factors influencing the choice)
- Current status (Proposed/Accepted/Deprecated/Superseded)

You can provide this in any format - bullet points, paragraphs, or structured sections.
```

Then extract information from the user's response and ask targeted follow-up questions only for critical missing pieces.

### Common Steps (Both Workflows)

2. **Analyze** - Examine the codebase to understand:
   - Current architecture and components
   - Affected files and modules
   - Existing ADRs (for numbering)

3. **Generate** - Create ADR document with:
   - Sequential ADR number
   - MADR-compliant structure
   - Evidence-based context
   - Clear decision statement
   - Documented alternatives
   - Positive and negative consequences

4. **Provide guidance** - Suggest:
   - Filename: `adr/ADR-XXX-title-in-kebab-case.md`
   - Where to store the file
   - How to update status over time

## Output Format

Generate an ADR following this MADR template:

```markdown
# ADR-XXX: [Decision Title]

Date: YYYY-MM-DD

## Status

[Proposed | Accepted | Deprecated | Superseded by ADR-YYY]

## Context

[Problem description, requirements, constraints]

## Decision Drivers

* [Factor 1]
* [Factor 2]
* [Factor 3]

## Considered Options

* [Option 1 - chosen]
* [Option 2]
* [Option 3]

## Decision Outcome

Chosen option: "[Option 1]", because [justification].

### Positive Consequences

* [Benefit 1]
* [Benefit 2]

### Negative Consequences

* [Challenge 1]
* [Challenge 2]

## Pros and Cons of the Options

### [Option 1]

* Good, because [argument a]
* Bad, because [argument b]

### [Option 2]

* Good, because [argument a]
* Bad, because [argument b]

## Links

* [Related ADR or documentation]
```

## Constraints

- **Evidence-based**: Reference actual code and file paths
- **Balanced**: Present alternatives fairly
- **Focused**: One decision per ADR
- **No speculation**: Ask for missing information
- **Sequential numbering**: Check existing ADRs to determine next number

## Storage Location

Default location: `adr/ADR-XXX-title-in-kebab-case.md`

If `adr/` doesn't exist, create it.
