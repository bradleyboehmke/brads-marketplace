---
description: Template for creating command files
---

# Command Template

Use this template when creating a new command for a plugin.

## Template Structure

```markdown
---
description: Brief description of what this command does (5-10 words)
---

[Opening context paragraph explaining what this command does and when to use it]

## Your Task

[Clear, specific description of the command's purpose and what it accomplishes]

## Step-by-Step Process

### Step 1: [First Step Name]

[Detailed instructions for this step]

**Actions to take:**
- [Specific action 1]
- [Specific action 2]
- [Specific action 3]

Wait for their response before proceeding. [If interactive]

### Step 2: [Second Step Name]

[Detailed instructions for this step]

**Actions to take:**
- [Specific action 1]
- [Specific action 2]

[Continue with additional steps as needed]

### Step N: [Final Step Name]

[Detailed instructions for final step]

**Expected outcome:**
- [What should be achieved]
- [What should be delivered]

## Important Notes

- [Important consideration 1]
- [Important consideration 2]
- [Important consideration 3]
- [Edge case or warning]

## [Optional: Advanced Options]

[If the command has advanced capabilities or configuration options]

## [Optional: Examples]

[If helpful, provide concrete examples of command usage]
```

## Example: Generate Tests Command

```markdown
---
description: Generates unit tests for existing code files
---

You are helping the user generate comprehensive unit tests for their code.

## Your Task

Analyze the user's code file(s) and generate appropriate unit tests with good coverage, edge cases, and clear assertions.

## Step-by-Step Process

### Step 1: Identify Target Code

Ask the user:
- Which file(s) should be tested?
- Are there specific functions/classes to focus on?
- What testing framework do they use?

Wait for their response before proceeding.

### Step 2: Analyze Code

Use the Read tool to examine the target code file(s).

**Look for:**
- Public functions/methods to test
- Input parameters and types
- Return values and types
- Edge cases and error conditions
- Dependencies and imports

### Step 3: Plan Test Coverage

For each function/method, identify:
- Happy path test cases
- Edge cases (empty inputs, null, boundary values)
- Error conditions (invalid inputs, exceptions)
- Integration points (mocked dependencies)

Present the test plan to the user and ask for confirmation.

### Step 4: Generate Test Code

Use the Write tool to create the test file.

**Include:**
- Proper test framework imports
- Setup/teardown if needed
- Descriptive test names
- Arrange-Act-Assert structure
- Mock setup for dependencies
- Clear assertions

### Step 5: Validate and Review

Review the generated tests:
- Check for syntax errors
- Verify all test cases are included
- Ensure tests are runnable
- Confirm good test naming

Present the test file to the user and offer to:
- Run the tests
- Add additional test cases
- Refine existing tests

## Important Notes

- Use the same testing framework as the project
- Follow the project's test naming conventions
- Place test files in the appropriate directory
- Mock external dependencies appropriately
- Aim for meaningful assertions, not just coverage numbers
- Test behavior, not implementation details

## Advanced Options

**Coverage Analysis:**
If requested, use coverage tools to identify untested code paths.

**Integration Tests:**
Can also generate integration tests that test multiple components together.

**Test Data:**
Can help create test fixtures or mock data as needed.

## Examples

**JavaScript/Jest:**
```javascript
describe('calculateTotal', () => {
  it('should sum array of numbers correctly', () => {
    expect(calculateTotal([1, 2, 3])).toBe(6);
  });

  it('should handle empty array', () => {
    expect(calculateTotal([])).toBe(0);
  });
});
```

**Python/pytest:**
```python
def test_calculate_total_with_numbers():
    assert calculate_total([1, 2, 3]) == 6

def test_calculate_total_with_empty_list():
    assert calculate_total([]) == 0
```
```

## Guidelines for Using This Template

### Frontmatter

**description field:**
- Must be 5-10 words
- Should clearly state what the command does
- Be action-oriented (use verbs)
- Be specific, not generic

**Examples:**
- ✅ "Generates unit tests for existing code files"
- ✅ "Scans codebase for security vulnerabilities"
- ✅ "Deploys application to Kubernetes cluster"
- ❌ "Helps with testing" (too vague)
- ❌ "Does stuff" (meaningless)

### Opening Context

**Purpose:** Set the stage for what the command does

**Guidelines:**
- 1-2 sentences
- Explain what and when
- Provide context

**Example:**
"You are helping the user generate comprehensive unit tests for their code. This command analyzes existing code files and creates test files with good coverage, edge cases, and clear assertions."

### Your Task Section

**Purpose:** Clear, specific goal statement

**Guidelines:**
- One paragraph
- Describe what will be accomplished
- Set expectations
- Be specific about outcomes

**Example:**
"Analyze the user's code file(s) and generate appropriate unit tests with good coverage, edge cases, and clear assertions."

### Step-by-Step Process

**Purpose:** Detailed workflow for Claude to follow

**Guidelines:**
- Clear, numbered steps
- Action-oriented step names
- Detailed instructions
- Tool usage specified (Read, Write, Bash, etc.)
- Wait points for user interaction (if applicable)

**Step Naming:**
- ✅ "Identify Target Code"
- ✅ "Analyze Code Structure"
- ✅ "Generate Test Cases"
- ❌ "Step 1" (not descriptive)
- ❌ "Do the thing" (vague)

**Step Content:**
- What to do
- How to do it
- What tools to use
- What to look for
- Expected output

**Interactive vs Automated:**
- Interactive: Include "Wait for their response"
- Automated: Process steps sequentially

### Important Notes Section

**Purpose:** Critical information, warnings, edge cases

**Guidelines:**
- 3-5 bullet points
- Highlight edge cases
- Warn about pitfalls
- Specify requirements
- Note constraints

**Examples:**
- "Use the same testing framework as the project"
- "Mock external dependencies appropriately"
- "Verify git status before making changes"

### Optional Sections

**Advanced Options:**
- For power users
- Optional features
- Configuration details

**Examples:**
- Code samples showing usage
- Before/after demonstrations
- Common scenarios

**Troubleshooting:**
- Common errors
- How to fix issues
- Debug strategies

## Command Types

### 1. Interactive Commands

Commands that require user input throughout.

**Characteristics:**
- Multiple "Wait for response" points
- Guided conversation
- User choices affect flow
- Examples: create-plugin, document-work

**Template pattern:**
```markdown
### Step 1: Ask User
Ask the user: [questions]
Wait for their response.

### Step 2: Process Response
Based on their answer: [actions]

### Step 3: Confirm
Present [options/plan] and ask for confirmation.
Wait for their response.
```

### 2. Automated Commands

Commands that run automatically with minimal input.

**Characteristics:**
- Minimal user interaction
- Sequential execution
- Clear inputs and outputs
- Examples: format-code, run-tests, deploy

**Template pattern:**
```markdown
### Step 1: Validate
Check prerequisites: [validations]

### Step 2: Execute
Run the operation: [actions]

### Step 3: Report
Present results: [output]
```

### 3. Analysis Commands

Commands that examine and report.

**Characteristics:**
- Read code/files
- Analyze patterns
- Generate reports
- Examples: scan-vulnerabilities, analyze-performance

**Template pattern:**
```markdown
### Step 1: Gather Data
Use Read tool to examine: [targets]

### Step 2: Analyze
Look for: [patterns/issues/metrics]

### Step 3: Report Findings
Present analysis: [structured report]
```

### 4. Generation Commands

Commands that create new files/code.

**Characteristics:**
- Create new content
- Use templates
- Write files
- Examples: generate-tests, scaffold-component

**Template pattern:**
```markdown
### Step 1: Gather Requirements
Ask about: [details needed]

### Step 2: Design Structure
Plan: [what will be created]

### Step 3: Generate Content
Use Write tool to create: [files]

### Step 4: Validate
Verify: [quality checks]
```

## Tool Usage

Specify which Claude Code tools to use:

**Read:** Reading files
```markdown
Use the Read tool to examine the target file:
`/path/to/file.js`
```

**Write:** Creating new files
```markdown
Use the Write tool to create the test file at:
`/path/to/file.test.js`
```

**Edit:** Modifying existing files
```markdown
Use the Edit tool to update the configuration:
[specify old_string and new_string]
```

**Bash:** Running commands
```markdown
Use the Bash tool to run the tests:
`npm test`
```

**Glob:** Finding files
```markdown
Use the Glob tool to find all test files:
Pattern: `**/*.test.js`
```

**Grep:** Searching content
```markdown
Use the Grep tool to find security issues:
Pattern: `eval\(|exec\(`
```

## Quality Checklist

Before finalizing a command:

- [ ] Frontmatter has 5-10 word description
- [ ] Opening context explains purpose
- [ ] Task section is clear and specific
- [ ] Steps are detailed and actionable
- [ ] Tool usage is specified
- [ ] Important notes cover edge cases
- [ ] Examples provided (if helpful)
- [ ] Wait points added for interactive commands
- [ ] Error handling considered
- [ ] Output clearly defined

## Common Mistakes to Avoid

❌ Vague instructions - "do something with the code"
❌ No tool specification - unclear how to accomplish tasks
❌ Missing edge cases - doesn't handle errors
❌ Too many steps - command is too complex (split it)
❌ No user interaction - automated when should be interactive
❌ No validation - doesn't check prerequisites
❌ Poor naming - step names not descriptive

## Tips for Writing Great Commands

1. **Be Explicit:** Specify exact tools and actions
2. **Handle Errors:** Consider what can go wrong
3. **Guide Users:** For interactive commands, ask good questions
4. **Validate:** Check prerequisites before proceeding
5. **Report Results:** Always show what was accomplished
6. **Be Consistent:** Follow the same patterns across commands
7. **Test It:** Run the command to ensure it works

## Validation

Test your command by:

1. Running it with typical inputs
2. Testing edge cases
3. Verifying error handling
4. Checking output quality
5. Getting user feedback
6. Refining based on results
