# 🎯 Commands

Commands are user-facing workflows that you invoke via slash command syntax. Each command activates an agent, loads required skills, and performs a specific task.

## Command Syntax

```bash
/plugin-name:command-name [--parameter=value]
```

**Examples:**
```bash
/git-workflow:draft-commit
/document-generator:generate-readme
/git-workflow:create-branch --issue=42
```

## All Available Commands

### git-workflow Commands

#### `/git-workflow:create-branch`

**Purpose:** Interactive branch creation following naming conventions

**Parameters:**
- `--issue=<number>` (optional) - GitHub issue number to link

**Workflow:**
1. Analyzes current branch and git status
2. Suggests branch name based on conventions (feature/, fix/, docs/, etc.)
3. Optionally fetches GitHub issue details
4. Creates and switches to new branch

**Output:** Console guidance + git branch creation

**Time:** 2-3 minutes

---

#### `/git-workflow:draft-commit`

**Purpose:** Generate standards-compliant commit message and create commit

**Parameters:** None

**Workflow:**
1. Analyzes git status (staged + unstaged changes)
2. Reviews git log for commit message style
3. Drafts commit message following Conventional Commits
4. Interactive approval/editing
5. Auto-stages files if needed
6. Creates commit

**Output:** Console + git commit

**Time:** 3-5 minutes

---

#### `/git-workflow:draft-pr`

**Purpose:** Generate PR title and description from branch changes

**Parameters:** None

**Workflow:**
1. Analyzes all commits since branch diverged from main
2. Reviews changed files and diffs
3. Drafts PR title and description
4. Interactive approval/editing
5. Optionally creates PR via `gh` CLI

**Output:** Console + optional PR creation

**Time:** 5-7 minutes

---

#### `/git-workflow:pre-commit-check`

**Purpose:** Run comprehensive pre-commit quality checks

**Parameters:** None

**Workflow:**
1. Detects project type and framework
2. Runs appropriate linters/formatters
3. Checks for common issues
4. Reports findings with actionable suggestions

**Output:** Console validation report

**Time:** 5-10 minutes

---

#### `/git-workflow:spec-issue`

**Purpose:** Transform GitHub issue into detailed implementation specification

**Parameters:**
- `--issue=<number>` (required) - GitHub issue number

**Workflow:**
1. Fetches issue details from GitHub
2. Analyzes codebase context
3. Creates detailed implementation plan
4. Interactive approval/editing
5. Optionally saves as file or posts to issue

**Output:** Console/file/GitHub comment

**Time:** 10-15 minutes

---

#### `/git-workflow:validate-commit`

**Purpose:** Validate commit message quality against standards

**Parameters:** None

**Workflow:**
1. Checks most recent commit message
2. Validates against Conventional Commits format
3. Provides feedback and suggestions

**Output:** Console validation report

**Time:** 1-2 minutes

---

#### `/git-workflow:validate-pr`

**Purpose:** Validate PR quality and readiness

**Parameters:** None

**Workflow:**
1. Analyzes current branch's PR readiness
2. Checks commit quality
3. Validates description completeness
4. Suggests improvements

**Output:** Console validation report

**Time:** 3-5 minutes

---

### document-generator Commands

#### `/document-generator:generate-readme`

**Purpose:** Create comprehensive README from scratch

**Parameters:** None

**Workflow:**
1. Analyzes project structure and code
2. Detects framework, dependencies, entry points
3. Generates README following best practices
4. Interactive approval/editing
5. Writes README.md

**Output:** README.md file

**Time:** 10-15 minutes

---

#### `/document-generator:update-readme`

**Purpose:** Update existing README with new information

**Parameters:** None

**Workflow:**
1. Reads existing README
2. Analyzes project for changes
3. Suggests specific updates
4. Interactive approval
5. Updates README.md

**Output:** Updated README.md

**Time:** 5-10 minutes

---

#### `/document-generator:validate-readme`

**Purpose:** Validate README against standards

**Parameters:** None

**Workflow:**
1. Checks for required sections
2. Validates completeness
3. Provides improvement suggestions

**Output:** Console validation report

**Time:** 2-3 minutes

---

#### `/document-generator:generate-changelog`

**Purpose:** Create new CHANGELOG.md from git history

**Parameters:** None

**Workflow:**
1. Analyzes git commit history
2. Groups by semantic version or date
3. Generates changelog following Keep a Changelog format
4. Interactive approval
5. Writes CHANGELOG.md

**Output:** CHANGELOG.md file

**Time:** 5-10 minutes

---

#### `/document-generator:update-changelog`

**Purpose:** Update existing changelog with recent commits

**Parameters:** None

**Workflow:**
1. Reads existing CHANGELOG.md
2. Analyzes commits since last entry
3. Drafts new entries
4. Interactive approval
5. Updates CHANGELOG.md

**Output:** Updated CHANGELOG.md

**Time:** 3-5 minutes

---

#### `/document-generator:validate-changelog`

**Purpose:** Validate changelog against Keep a Changelog format

**Parameters:** None

**Workflow:**
1. Checks changelog structure
2. Validates versioning format
3. Ensures proper categorization
4. Provides improvement suggestions

**Output:** Console validation report

**Time:** 2-3 minutes

---

#### `/document-generator:generate-adr`

**Purpose:** Create Architecture Decision Record in MADR format

**Parameters:** None

**Workflow:**
1. Interactive interview about the decision
2. Gathers context, options, consequences
3. Generates MADR-compliant ADR
4. Interactive approval
5. Saves to appropriate directory

**Output:** .md file in ADR directory

**Time:** 5-10 minutes

---

#### `/document-generator:generate-architecture-diagram`

**Purpose:** Create Mermaid architecture diagram

**Parameters:** None

**Workflow:**
1. Interactive diagram type selection (C4, flowchart, sequence, ER, etc.)
2. Analyzes codebase for architecture
3. Generates Mermaid diagram
4. Interactive approval
5. Inserts into existing file or creates standalone

**Output:** Mermaid diagram in .md file

**Time:** 10-15 minutes

---

### marketplace-dev Commands

#### `/marketplace-dev:design-plugin`

**Purpose:** Design new plugin architecture following marketplace principles

**Parameters:** None

**Workflow:**
1. Interactive interview about plugin purpose
2. Identifies reusable skills from existing plugins
3. Designs agent/skill/command structure
4. Generates implementation plan with token estimates
5. Creates development checklist

**Output:** Console architecture plan

**Time:** 15-20 minutes

---

#### `/marketplace-dev:review-plugin`

**Purpose:** Review plugin for redundancy, verbosity, and standards compliance

**Parameters:** None

**Workflow:**
1. Analyzes plugin components
2. Checks for redundant content
3. Identifies verbose instructions
4. Validates architecture patterns
5. Provides refactoring suggestions

**Output:** Console review report

**Time:** 10-15 minutes

---

#### `/marketplace-dev:update-plugin-docs`

**Purpose:** Verify and update marketplace documentation

**Parameters:** None

**Workflow:**
1. Scans all plugins for commands, agents, skills
2. Cross-references with marketplace docs
3. Identifies missing or outdated documentation
4. Generates update proposals
5. Interactive approval to update docs

**Output:** Updated documentation files

**Time:** 5-10 minutes

---

### note-taker Commands

#### `/note-taker:document-work`

**Purpose:** Create structured note from work session

**Parameters:** None

**Workflow:**
1. Analyzes conversation history and git commits
2. Interactive organization/template selection
3. Interactive save location selection
4. Generates content for each template field
5. Field-by-field review and approval
6. Saves note with automatic filename

**Output:** .md note file with timestamp

**Time:** 5-10 minutes

---

### course-builder Commands

#### `/course-builder:write-chapter`

**Purpose:** Write textbook chapter for data science course

**Parameters:** None

**Workflow:**
1. Interactive course and topic selection
2. Analyzes course profile and standards
3. Generates chapter content with examples
4. Interactive review and editing
5. Saves chapter file

**Output:** .md chapter file

**Time:** 30-45 minutes

---

#### `/course-builder:review-chapter`

**Purpose:** Review chapter for technical accuracy, clarity, and quality

**Parameters:** None

**Workflow:**
1. Reads existing chapter
2. Checks technical accuracy
3. Validates against course standards
4. Provides improvement suggestions
5. Generates review report

**Output:** Console review report

**Time:** 10-15 minutes

---

#### `/course-builder:create-companion-nb`

**Purpose:** Create companion Jupyter notebook for chapter

**Parameters:** None

**Workflow:**
1. Reads chapter content
2. Extracts code examples and concepts
3. Creates interactive notebook with exercises
4. Includes solutions in comments
5. Saves .ipynb file

**Output:** .ipynb notebook file

**Time:** 15-20 minutes

---

#### `/course-builder:create-lab-nb`

**Purpose:** Create lab assignment Jupyter notebook

**Parameters:** None

**Workflow:**
1. Interactive lab topic and difficulty selection
2. Generates assignment with scaffolding
3. Creates solution notebook separately
4. Includes grading rubric
5. Saves assignment and solution files

**Output:** Assignment .ipynb + solution .ipynb

**Time:** 20-30 minutes

---

#### `/course-builder:create-quiz`

**Purpose:** Create reading comprehension quiz from chapter

**Parameters:** None

**Workflow:**
1. Reads chapter content
2. Identifies key concepts
3. Generates multiple-choice questions
4. Creates answer key
5. Saves quiz file

**Output:** Quiz .md file with answers

**Time:** 10-15 minutes

---

#### `/course-builder:create-slides`

**Purpose:** Create presentation slides for lecture

**Parameters:** None

**Workflow:**
1. Interactive topic and course selection
2. Analyzes chapter or topic outline
3. Generates slide deck with structure
4. Includes code examples and visualizations
5. Saves slides file

**Output:** .md slides file

**Time:** 20-30 minutes

---

#### `/course-builder:create-module-overview`

**Purpose:** Create Canvas module overview document

**Parameters:** None

**Workflow:**
1. Interactive module topic selection
2. Gathers learning objectives
3. Creates structured overview
4. Includes resource links
5. Saves overview file

**Output:** .md module overview

**Time:** 10-15 minutes

---

#### `/course-builder:create-ta-guide`

**Purpose:** Create TA guidance with solutions and teaching strategies

**Parameters:** None

**Workflow:**
1. Reads lab or assignment
2. Creates comprehensive solutions
3. Identifies common student mistakes
4. Provides teaching tips
5. Saves TA guide

**Output:** .ipynb TA guide

**Time:** 15-20 minutes

---

## Command Patterns

### Interactive Commands

Most commands use interactive workflows:
1. Analyze current context
2. Present findings and proposal
3. Interactive approval/editing
4. Execute action (write file, create commit, etc.)

### Standards-Based Commands

Commands that enforce standards:
- Conventional Commits (git-workflow)
- Keep a Changelog (document-generator)
- MADR format (document-generator)
- README best practices (document-generator)

### File-Generating Commands

Commands that create files:
- Auto-generate appropriate filenames
- Place in conventional locations
- Follow industry format standards
- Support interactive editing before saving

## Next Steps

- See [Agents](./agents.md) for domain expert capabilities
- See [Skills](./skills.md) for knowledge modules
- See [Usage Guide](../usage.md) for workflow examples
