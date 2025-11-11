---
description: Create detailed implementation specification from a GitHub issue through interactive planning
---

# Spec Issue Command

You are helping a developer create a **detailed implementation specification** from a GitHub issue.

## Command Parameters

**Issue Parameter:**
- `--issue=<number>` - GitHub issue number (optional - will prompt if not provided)

**Repository Parameter:**
- `--repo=<owner/repo>` - Repository (default: auto-detect from git remote)

**Usage Examples:**
```bash
/git-workflow:spec-issue                    # Interactive - prompts for issue
/git-workflow:spec-issue --issue=15         # Spec for issue #15
/git-workflow:spec-issue --issue=22 --repo=owner/repo  # Specify repo
```

## Objective

Transform a high-level GitHub issue into a detailed, actionable implementation specification including:
- Overview and scope
- Architecture decisions and rationale
- Component design breakdown
- File structure
- Phased implementation checklist
- Technical considerations
- Next steps

## Activated Agent

**Activate**: `git-workflow-specialist` agent

## Activated Skills

- **`github-workflow-patterns`** - For GitHub best practices and workflows
- **`github-issue-analysis`** - For understanding issue structure and prioritization

## Process

### Step 0: Issue Selection

If `--issue` parameter is not provided, help user select an issue interactively.

#### Fetch Recent Issues

```bash
# List recent open issues
gh issue list --limit 20 --json number,title,labels,createdAt
```

#### Present Issue List

Display issues in a clear, scannable format:

```
Which issue would you like to create a spec for?

Recent open issues:
 1. #22 - Define scripts for programmatic auditing checks [enhancement]
 2. #21 - Compare performance using different models
 3. #20 - Plugin creation through GH issue workflow
 4. #17 - MCP Confluence Integration
 5. #15 - Add Git-Workflow Plugin [enhancement, git, github]
 6. #14 - Outline Python-Dev Plugin for personal use Marketplace [enhancement]
 ...

Enter issue number (or 'cancel' to exit):
```

**User provides number:**
- Validate the number exists in the list
- If valid, proceed to Step 1
- If invalid, show error and re-prompt

**User types 'cancel':**
- Exit gracefully: "Spec creation cancelled."

#### If --issue Provided

Skip the selection step and proceed directly to Step 1 with the provided issue number.

---

### Step 1: Fetch Issue Details

Once issue number is selected, fetch complete issue information:

```bash
# Fetch issue with all details
gh issue view <number> --json title,body,labels,comments,createdAt,updatedAt
```

**Parse and display:**

```
Fetching issue #<number>...
✓ Issue loaded

Title: <issue-title>
Labels: [label1, label2, ...]
Created: <date>

Description:
<issue-body>

Comments: <number> comments
[Optionally show recent comments if relevant to planning]

Ready to create specification for this issue.
```

**Validate issue exists:**
- If issue not found: "❌ Issue #<number> not found. Please check the issue number."
- Exit gracefully

### Step 2: Interactive Planning

Ask clarifying questions to understand the implementation approach. Adapt questions based on issue content and labels.

#### Question 1: Implementation Type

```
What type of implementation is this?
1. 🔌 New plugin
2. 📝 New command in existing plugin
3. ✨ Feature enhancement to existing component
4. 🔧 Refactoring/improvement
5. 📚 Documentation

Enter choice (1-5):
```

#### Question 2: Architecture Pattern (if applicable)

For plugins or complex features:

```
What architecture pattern should we use?
1. Workflow Orchestration + Agent + Skills (complex, interactive workflows)
2. Commands + Skills (moderate complexity, reusable patterns)
3. Commands only (simple, standalone functionality)

Enter choice (1-3):
```

#### Question 3: Core Capabilities

```
Describe the core capabilities needed (1-2 sentences):
[User input]
```

#### Question 4: Components Needed

Based on architecture choice, ask about specific components:

**For Agent + Skills + Commands:**
```
What components are needed?
- Agent name/role:
- Skills (comma-separated):
- Commands (comma-separated):
```

**For Commands + Skills:**
```
What components are needed?
- Commands (comma-separated):
- Skills (comma-separated, if any):
```

#### Question 5: Implementation Phases

```
How should implementation be phased?
1. Single phase (implement all at once)
2. Multiple phases (specify below)

[If multiple phases]
Describe phases (one per line):
Phase 1:
Phase 2:
...
```

#### Question 6: Technical Constraints

```
Any technical constraints or considerations? (optional)
- Token budgets?
- Performance requirements?
- Integration dependencies?
[User input or skip]
```

**Store all answers** to use in spec generation (Step 3).

### Step 3: Generate Specification

Using answers from Step 2 and the issue details, generate a comprehensive specification document.

#### Spec Structure

```markdown
# [Issue Title] - Implementation Specification

**Generated**: [date]
**Status**: Design Specification for Implementation

---

## Overview

**Purpose**: [From core capabilities answer]

**Use Cases**:
- [Extracted from issue or inferred]

**Scope**:
- **Included**: [What will be implemented]
- **Excluded**: [What is out of scope, if any]

---

## Architecture Decision

**Pattern**: [From Question 2 answer]

**Rationale**:
[Explain why this pattern was chosen based on requirements]

**Benefits**:
- [List key benefits of this approach]

---

## Component Design

[Based on architecture choice - include agents, skills, commands sections]

### Agent (if applicable)
- **Name**: [agent-name]
- **Role**: [description]
- **Responsibilities**: [what it does]

### Skills (if applicable)
For each skill:
- **Name**: [skill-name]
- **Purpose**: [what it provides]
- **Used By**: [which components use it]

### Commands
For each command:
- **Name**: [command-name]
- **Purpose**: [what it does]
- **Parameters**: [list parameters]
- **Workflow**: [high-level flow]

---

## File Structure

\```
[directory tree of files to create]
\```

---

## Implementation Checklist

[Generate phases from Question 5]

### Phase 1: [name]
- [ ] Task 1
- [ ] Task 2

### Phase 2: [name]
- [ ] Task 1

---

## Technical Considerations

[From Question 6 or inferred from issue]

---

## Next Steps

1. Review specification
2. [Additional steps based on context]
```

**Generate this spec** based on all gathered information.

### Step 4: Output Options

Present interactive output options:

```
✓ Specification generated successfully!

What would you like to do with this spec?
1. 📄 Write to markdown file
2. 💬 Post as comment to GitHub issue #<number>
3. 📺 Display in terminal only
4. ✅ Both - write to file AND post to issue

Enter your choice (1-4):
```

| Option | Actions | Commands |
|--------|---------|----------|
| **1. Write to File** | Prompt for path (default: `./specs/issue-<number>-spec.md`)<br>Create `specs/` directory<br>Write spec to file | `mkdir -p specs`<br>`cat > path <<'EOF' [spec] EOF` |
| **2. Post to Issue** | Post spec as comment to GitHub issue | `gh issue comment <number> --body "[spec]"` |
| **3. Display Only** | Print full spec to console<br>No file/issue creation | *(Display spec content)* |
| **4. Both** | Execute options 1 AND 2<br>Prompt for path, write file, post to issue | *(Combine 1 + 2)* |

**Confirmation messages** (after execution):
- Option 1: `✓ Spec written to [path]`
- Option 2: `✓ Spec posted to https://github.com/<owner>/<repo>/issues/<number>`
- Option 3: `Note: Spec displayed only (not saved)`
- Option 4: Both confirmations from 1 + 2

---

## Important Notes

- **Be thorough**: Generate comprehensive specs that answer implementation questions
- **Be specific**: Include concrete component names, file paths, and task breakdowns
- **Be helpful**: Provide context and rationale for decisions
- **Be flexible**: Adapt structure based on implementation type
- **Ask when unclear**: If issue is vague, ask clarifying questions

## Error Handling

**Issue not found:**
```
❌ Issue #<number> not found in this repository.

Check:
- Issue number is correct
- You have access to this repository
- Issue hasn't been deleted

Try: gh issue list
```

**gh command not available:**
```
❌ GitHub CLI (gh) is not installed or not authenticated.

Install: https://cli.github.com/
Authenticate: gh auth login

Cannot proceed without gh CLI.
```

**Invalid input:**
```
❌ Invalid choice. Please enter 1, 2, 3, or 4.
[Re-prompt]
```

---

**Remember**: This command transforms ideas into actionable plans. Be thorough, ask good questions, and generate clear specifications that make implementation straightforward.

---

**Remember**: This command is fully interactive and guides users through creating comprehensive specs without requiring them to know all parameters upfront.
