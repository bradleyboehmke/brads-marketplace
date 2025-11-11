# Content Generation Strategies

This skill provides guidance on how to analyze work sessions and generate high-quality content for documentation templates.

## Information Sources

### Primary: Claude Code Conversation History

This is your richest source of information. The conversation contains:
- **Discussions about goals and intent** - Why the work was needed
- **Design decisions and trade-offs** - How approaches were chosen
- **Problem-solving iterations** - Challenges faced and solutions developed
- **Technical details and explanations** - Implementation specifics
- **Context and reasoning** - The "why" behind the "what"
- **Future considerations** - Next steps and TODOs mentioned

### Secondary: Git Repository Data

Use git to supplement and validate the conversation:
- **Today's commits:** `git log --since="today" --pretty=format:"%h - %s (%an)" --no-merges`
- **Changed files:** `git diff --name-only HEAD@{1.day.ago}..HEAD`
- **Commit messages:** Capture what was done
- **File patterns:** Show scope of changes

If no git data is available, rely entirely on conversation context.

## Field-by-Field Generation Strategy

### Date Field
Auto-fill with today's date in YYYY-MM-DD format. No user prompt needed.

### Title/Name Fields
**Strategy:** Combine project name with work type
**Sources:** User-provided project name + conversation about what was built
**Example:** "Plugin Architecture Refactoring" from project name "plugin-refactor"

### Goal/Objective Fields
**Strategy:** Extract the "why" from the conversation
**Look for:**
- Problem statements at the beginning of the session
- User requests and requirements
- Pain points mentioned
- Desired outcomes discussed

**Example:** "Restructure the note-taker plugin to align with marketplace architecture principles and improve modularity"

### Approach/How Fields
**Strategy:** Describe the technical approach and methodology
**Look for:**
- Design decisions made during the conversation
- Technologies and tools used
- Architecture patterns discussed
- Implementation steps taken
- Files and components created

**Example:** "Broke the monolithic command into agents, commands, and skills pattern. Created documentation-assistant agent for expertise, organization-config skill for dynamic discovery, and simplified command for orchestration."

### Results/Outcomes Fields
**Strategy:** Summarize what was successfully accomplished
**Look for:**
- Features or code completed
- Problems solved
- Artifacts created
- Tests passing
- Successful builds or deployments

**Example:** "Successfully restructured plugin with 4 new files: agent, 2 skills, updated command. Reduced command from 189 lines to ~60. Implemented dynamic template discovery."

### Challenges/Blockers Fields
**Strategy:** Identify difficulties and how they were resolved
**Look for:**
- Errors encountered
- Unexpected behaviors
- Decisions that required debate
- Problems that needed creative solutions
- Anything marked as "tricky" or "challenging"

**Example:** "Initial approach used hardcoded template lists. Refactored to use Glob for dynamic discovery to improve maintainability."

### Next Steps/Future Work Fields
**Strategy:** Extract forward-looking items
**Look for:**
- TODOs mentioned
- Features deferred
- Ideas for improvements
- Follow-up tasks identified
- Testing or validation needed

**Example:** "Update documentation to reflect new structure. Test template discovery with actual files. Consider adding validation for template fields."

## Content Generation Process

### Step 1: Analyze the Full Session
Review the entire conversation history to understand:
- What was the initial request?
- What was discussed and decided?
- What was implemented?
- What challenges came up?
- What was the outcome?

### Step 2: Supplement with Git Data
If available, use git commits to:
- Validate what files were changed
- See commit messages for additional context
- Understand scope of changes

### Step 3: Generate Field Content
For each template field:
1. Identify what type of information is needed
2. Extract relevant details from conversation + git
3. Synthesize into clear, specific content
4. Make it detailed enough to be useful

### Step 4: Present for Approval
Format:
```
[Field Name]:
Your proposed content here...

Accept this? (Press Enter to accept, or type your changes)
```

Default behavior is acceptance - make content good enough to just press Enter.

## Quality Guidelines

**Be Specific:**
- Use actual file names, feature names, technical terms
- Include numbers when relevant (lines of code, number of files, etc.)
- Reference specific technologies and approaches

**Be Comprehensive:**
- Capture both what and why
- Include context that might be forgotten later
- Don't just list actions, explain reasoning

**Be Concise:**
- Focus on important details
- Avoid unnecessary verbosity
- Make every sentence count

**Be Accurate:**
- Base proposals on actual conversation and git data
- Don't invent or assume information
- If uncertain, ask the user

## Example: Full Template Fill

**Template Field:** What did you build?
**Generated Content:** "Restructured the note-taker plugin from a single 189-line command into a modular architecture with agent, commands, and skills. Created documentation-assistant agent for note-taking expertise, organization-config skill for dynamic template discovery, and content-generation skill for analysis strategies. Reduced command file to ~60 lines focused on workflow orchestration."

**Why this is good:**
- Specific numbers (189 lines → 60 lines)
- Named components created
- Explained the transformation
- Clear outcome
- Based on actual conversation
