---
description: Reviews a textbook chapter for technical accuracy, clarity, tone, style, and grammar based on course standards.
---

# Review Textbook Chapter

This command leverages the `course-architect` agent to perform a comprehensive review of a textbook chapter, ensuring it aligns with the specific course's pedagogical standards and style.

The agent will analyze the chapter based on the detected or selected course profile and provide specific, actionable feedback on:
* Technical Accuracy (code & concepts)
* Clarity for Beginners (using course profile audience)
* Tone Alignment (encouraging, practical, conversational)
* Pedagogical Elements (use of callouts, examples, checks)
* Sentence Case Compliance (for markdown headings)
* Grammar and Flow

## Interactive Workflow

### Step 1: Course Detection and Selection

Attempt to automatically detect the course based on the current working directory path.

**Agent Action:**
* Get the current working directory path (e.g., using `pwd` in Bash).
* Check if the path contains `bana-4080`, `bana-6043`, or `bana-7075`.

**If course detected:**
```
Detected course: BANA [XXXX] based on the current directory.

[1] Confirm BANA [XXXX]
[2] Select a different course

Please select an option:
```
If [1], proceed with the detected course. If [2], show the manual selection prompt below.

**If no course detected OR user selects [2]:**
```
Which course is this chapter for?

[1] BANA 4080 (Intro to Data Mining - Undergraduate)
[2] BANA 6043 (Statistical Computing - Graduate)
[3] BANA 7075 (ML in Business - Graduate)

Please select an option by number:
```

**Agent Action (Post-Selection):**
* Load the appropriate **course profile** (e.g., `intro-to-data-mining/course-profile.md`).
* Load the `pedagogy/teaching-principles.md` skill.

### Step 2: Chapter Input

Ask the user for the chapter content file:

```
Please provide the path to the chapter file (.qmd or .md) you want me to review:
(e.g., /path/to/book/chapter-5.qmd)
```

**Agent Action:**
* Read the full content of the specified file.

### Step 3: Review and Generate Feedback

The agent analyzes the entire chapter based on the loaded course profile and pedagogical principles.

**Agent Actions:**
* Load relevant course context from the course profile
* Parse the chapter structure (headings, sections, code blocks, callouts)
* Evaluate against the following criteria:

**Review Criteria:**

1. **Technical Accuracy**
   - Verify code examples run correctly and follow best practices
   - Check that concepts are explained accurately
   - Ensure libraries/functions are used appropriately
   - Validate that examples align with the course's technical stack

2. **Clarity for Beginners (Audience-Specific)**
   - Assess whether explanations match the target audience level (from course profile)
   - Check for assumed knowledge that hasn't been introduced
   - Verify that jargon is either avoided or clearly defined
   - Ensure examples build progressively in complexity

3. **Tone Alignment**
   - Verify the tone matches course standards (e.g., conversational, encouraging)
   - Check that the chapter is practical and business-focused (if applicable)
   - Ensure the writing is engaging and motivating
   - Assess whether the chapter reduces anxiety and builds confidence

4. **Pedagogical Elements**
   - Verify presence of learning objectives
   - Check for appropriate use of callouts (tips, warnings, notes)
   - Assess quality and relevance of examples
   - Verify inclusion of check-your-understanding questions
   - Ensure proper spacing of practice opportunities

5. **Sentence Case Compliance (Headings)**
   - Check all markdown headings (##, ###, ####) use sentence case
   - Flag any title case headings
   - Provide specific examples of violations

6. **Grammar and Flow**
   - Check for grammatical errors
   - Assess logical flow between sections
   - Verify smooth transitions
   - Check for consistency in terminology

### Step 4: Present Feedback Report

Display the comprehensive review to the user, structured by category.

```
Here is the review for [chapter-file.qmd], evaluated against BANA [XXXX] standards:

## Overall Assessment

[Summary paragraph providing high-level evaluation]

-----

## 1. Technical Accuracy

  * **Status:** [✅ Excellent / ⚠️ Needs Attention / ❌ Issues Found]
  * **Feedback:** [Specific points with line numbers or section references]

-----

## 2. Clarity for Beginners (Audience: BANA [XXXX])

  * **Status:** [✅ Excellent / ⚠️ Needs Attention / ❌ Issues Found]
  * **Feedback:** [Specific points with examples]

-----

## 3. Tone Alignment (Target: [e.g., Conversational, Encouraging])

  * **Status:** [✅ Excellent / ⚠️ Needs Attention / ❌ Issues Found]
  * **Feedback:** [Specific points with examples]

-----

## 4. Pedagogical Elements

  * **Status:** [✅ Excellent / ⚠️ Needs Attention / ❌ Issues Found]
  * **Feedback:** [Specific points about callouts, examples, exercises]

-----

## 5. Sentence Case Compliance (Headings)

  * **Status:** [✅ Compliant / ❌ Violations Found]
  * **Feedback:** [List specific headings that need correction]

-----

## 6. Grammar and Flow

  * **Status:** [✅ Excellent / ⚠️ Needs Attention / ❌ Issues Found]
  * **Feedback:** [Specific points about grammar or flow issues]

-----

What would you like to do with this feedback?

[1] Save report as a GitHub Issue
[2] Address these issues now (edit chapter)
[3] Discard

Please select an option:
```

### Step 5: Save as GitHub Issue (If user selects [1])

**Agent Action:**
1. Ask for confirmation on the repository (try to infer from the current directory's git remote).
    ```
    I can create a GitHub issue in the repository associated with this directory: [repo name].

    Issue Title Suggestion: "Chapter Review Feedback: [chapter-file.qmd]"

    [1] Create issue with this title in [repo name]
    [2] Edit title before creating
    [3] Cancel
    ```
2. If confirmed, format the feedback report from Step 4 into markdown suitable for a GitHub issue body.
3. **Create the GitHub issue** using the `gh` CLI tool via Bash:
    ```bash
    gh issue create --title "Chapter Review Feedback: [chapter-file.qmd]" --body "$(cat <<'EOF'
    [Formatted feedback report]
    EOF
    )"
    ```
4. Display confirmation: `✅ GitHub issue created successfully at [link to issue]` or provide fallback instructions if `gh` is not available.

### Step 6: Address Issues Now (If user selects [2])

**Agent Action:**
1. Ask how the user wants to proceed:
    ```
    How would you like to address the feedback?

    [1] Address all issues sequentially (guided edits)
    [2] Focus on specific issues (you tell me where to start)
    [3] Try to address all issues at once (agent makes edits, you review)
    [4] Cancel

    Please select an option:
    ```
2. **Based on selection:**
    * **[1] Sequential:**
        * Go through each feedback point category by category (e.g., starting with Technical Accuracy).
        * For each issue within a category:
            - State the specific issue
            - Propose a fix
            - Use the Edit tool to make the change to the chapter file
            - Show the change to the user for approval
        * Repeat for the next feedback category.
    * **[2] Specific:**
        * Ask the user: "Which feedback point (e.g., 'Clarity issue in Section 3.2' or 'Sentence case violation in heading') would you like to address first?"
        * Follow the same process as Sequential, but only for the user-selected issues.
    * **[3] All at Once:**
        * Propose revising the entire chapter based on all feedback points
        * Use the Edit tool or Write tool to make comprehensive changes
        * Present a summary of changes made
        * Ask user to review the updated chapter
    * **[4] Cancel:** End the workflow.
3. After edits (if any) are completed:
    ```
    ✅ Chapter edits based on feedback are complete.

    Would you like to:
    [1] Review the chapter again to verify improvements
    [2] Exit
    ```

### Step 7: Discard (If user selects [3])

**Agent Action:**
* Display confirmation: `Feedback discarded. No changes made.`
* End the workflow.

## What the Agent Does

The course-architect agent will:

**Analysis Phase:**
- Load appropriate course profile based on selection
- Read the entire chapter file
- Parse structure and identify all components (headings, code, callouts, etc.)
- Gather context about course standards and expectations

**Review Phase:**
- Systematically evaluate each review criterion
- Document specific issues with location references (section names, line numbers)
- Assess severity of each issue
- Compile comprehensive feedback organized by category

**Reporting Phase:**
- Present structured feedback report
- Provide status indicators for each category
- Include specific, actionable recommendations
- Guide user through post-review options

**Action Phase (if user chooses to address feedback):**
- Make precise edits to the chapter file
- Maintain original formatting and structure
- Apply fixes based on the documented feedback
- Verify changes align with course standards

## Skills Available to Agent

The agent has access to:
- **pedagogy**: Teaching principles and pedagogical best practices
- **content-templates**: Chapter and content structure patterns
- **courses/bana-4080**: BANA 4080 course profile and standards
- **courses/bana-6043**: BANA 6043 course profile and standards
- **courses/bana-7075**: BANA 7075 course profile and standards

## Output

A comprehensive review report including:
- Overall assessment summary
- Detailed feedback across six key dimensions
- Specific examples and location references
- Status indicators (✅/⚠️/❌) for each category
- Actionable recommendations
- Interactive options for handling feedback (GitHub issue, immediate edits, or discard)

**Post-Review Actions:**
- Optional GitHub issue creation with formatted feedback
- Optional guided editing workflow to address feedback
- Re-review capability to verify improvements
