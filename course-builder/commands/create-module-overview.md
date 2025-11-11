---
description: Create a Canvas module overview document
---

# Create Module Overview

Generate a Canvas module overview document that summarizes the week's learning objectives, content, and activities.

## Interactive Workflow

This command uses a numbered-option interactive workflow to gather requirements and create the module overview.

### Step 1: Course Selection

Ask the user which course this module overview is for:

```
Which course is this module overview for?

[1] BANA 4080 (Intro to Data Mining - Undergraduate)
[2] BANA 6043 (Statistical Computing - Graduate)
[3] BANA 7075 (ML in Business - Graduate)

Please select an option by number:
```

Load the appropriate course profile.

### Step 2: Module Number

Ask what module/week this overview is for:

```
What module/week number is this overview for?
(e.g., 4, 6, 10)
```

### Step 3: Content References

Ask which content materials to include:

```
Which chapters should be referenced for this module?
(Provide chapter numbers or names, e.g., "Chapters 7-9" or "Control Flow, Functions")
```

Then ask:

```
Path to Tuesday lecture slides (or description of lecture topics):
(Press Enter to skip if not available)
```

Then ask:

```
Path to Thursday lab notebook (or description of lab activities):
(Press Enter to skip if not available)
```

### Step 4: Analyze Content

Read and analyze the provided materials:
- If chapter paths are provided, read the chapters to extract learning objectives and key concepts
- If slide path is provided, read the slides to understand lecture structure
- If lab path is provided, read the lab to understand hands-on activities
- Extract module title from content (e.g., "Control Flow, Iteration, and Functions")
- Identify learning objectives (aim for 5-8 measurable objectives)
- Extract key concepts and skills for "What You'll Learn This Week"
- Summarize Tuesday lecture and Thursday lab activities

### Step 5: Supplemental Files

Ask about supplemental files:

```
Are there any supplemental files or materials to include?
(e.g., companion notebooks, example code, additional resources)

[1] No, leave as "TBD"
[2] Yes, I'll provide details

Please select an option:
```

If option [2], ask:

```
Please list the supplemental files and materials to include:
(e.g., "Chapter 23 Logistic Regression Notebook: link", "Reading Quiz: Available Monday-Wednesday")
```

### Step 6: Generate Overview

Using the template at `/Users/b294776/Desktop/UC/uc-bana-4080/planning/templates/module_overview_template.md`, generate the module overview by:

1. Reading the template file
2. Replacing all `{PLACEHOLDERS}` with content extracted from analysis:
   - `{MODULE_NUMBER}` - Week/module number
   - `{MODULE_TITLE}` - Descriptive title extracted from content
   - `{MODULE_TOPIC_BLURB}` - 2-3 paragraph overview connecting technical content to business context
   - `{LEARNING_OBJECTIVE_X}` - Specific, measurable learning objectives (5-8 items)
   - `{KEY_POINT_X}` - Concise bullets highlighting skills/concepts from "What You'll Learn"
   - `{TUESDAY_LECTURE_TITLE}` - Title of Tuesday's lecture
   - `{TUESDAY_LECTURE_ACTIVITIES}` - 2-4 bullets describing lecture activities
   - `{THURSDAY_LAB_TITLE}` - Title of Thursday's lab
   - `{THURSDAY_LAB_ACTIVITIES}` - 2-4 bullets describing lab activities
   - Supplemental files section (TBD or user-provided content)

3. Ensure tone is:
   - Approachable and practical
   - Business-focused
   - Encouraging
   - Concrete with specific examples

4. Remove all HTML comments and guidance text from the final output

### Step 7: Present Draft

Display the complete generated overview to the user:

```
Here's the proposed module overview:

───────────────────────────────────────────
[Full generated overview text]
───────────────────────────────────────────

Does this look good?

[1] Yes, save this overview
[2] No, I'd like to make changes

Please select an option:
```

If option [2], ask:

```
What changes would you like me to make?
```

Then regenerate with the requested changes and present again.

### Step 8: Save Location

When user accepts the overview, ask where to save:

```
Where should I save the module overview?

[Suggested: /Users/b294776/Desktop/UC/uc-bana-4080/planning/canvas_docs/]

Please provide the directory path (or press Enter to use suggested path):
```

Then ask for filename:

```
What should I name the file?
[Suggested: week{X}_overview.md]

Please provide the filename (or press Enter to use suggested name):
```

Save the file and display confirmation.

### Step 9: Completion Message

```
✅ Module overview created successfully!

Location: [full path to created file]

The overview includes:
- Module topic introduction with business context
- {X} learning objectives
- "What You'll Learn This Week" summary
- Tuesday lecture and Thursday lab descriptions
- Supplemental files section

Next steps:
- Review the overview in your editor
- Copy and paste into Canvas module page
- Add any course-specific formatting or links
```

## What the Agent Does

The course-architect agent will:

**Analysis Phase:**
- Load appropriate course profile
- Read and analyze provided chapters, slides, and lab materials
- Extract key learning objectives from content
- Identify core concepts and skills
- Understand Tuesday lecture structure and activities
- Understand Thursday lab structure and activities

**Content Generation:**
- Read the module overview template
- Generate engaging 2-3 paragraph module topic introduction
- Create 5-8 specific, measurable learning objectives
- Write concise, business-focused "What You'll Learn" bullets
- Summarize Tuesday lecture activities (2-4 bullets)
- Summarize Thursday lab activities (2-4 bullets)
- Include supplemental files if provided
- Maintain consistent structure across all weeks

**Quality Assurance:**
- Ensure tone is approachable and business-focused
- Verify all placeholders are replaced
- Check that learning objectives are measurable
- Confirm activities are described concretely
- Remove all guidance comments
- Present for user review before saving

## Course-Specific Requirements

### BANA 4080 (Undergraduate)
- **Template:** Must use the provided template exactly
- **Tone:** Approachable, encouraging, practical
- **Business Context:** Strong emphasis on real-world business applications
- **Examples:** Concrete, relatable scenarios (customer data, marketing, retail)
- **Structure:** Consistent week-to-week format for Canvas

### BANA 6043 & 7075 (Graduate)
- **Tone:** More formal but still engaging
- **Business Context:** Advanced applications, research scenarios
- **Examples:** Complex business problems, industry case studies
- **Structure:** Adapt template to graduate-level expectations

## Template Structure

The overview follows this structure:

1. **Module Title**: Module X Overview: [Topic]
2. **Module Topic**: 2-3 paragraphs connecting technical content to business context
3. **Learning Objectives** (🎯): 5-8 measurable objectives with action verbs
4. **What You'll Learn This Week** (✅): Concise bullet list of key concepts/skills
5. **How You'll Practice** (🛠): Tuesday lecture + Thursday lab descriptions
6. **Lectures & Other Supplemental Files** (📂): Readings, assessments, notebooks, links

## Key Principles

**Content Extraction:**
- Learning objectives should align with chapter/lecture/lab content
- "What You'll Learn" should be concrete and specific
- Practice activities should emphasize hands-on application
- Business relevance should be clear throughout

**Writing Style:**
- Use active voice and action verbs
- Keep examples concrete and relatable
- Emphasize practical application over theory
- Maintain encouraging, supportive tone
- Connect concepts to career skills

**Quality Checks:**
- All placeholders filled with specific content
- No generic or vague statements
- Business context present throughout
- Consistent with course profile tone and standards
- User reviewed and approved before saving

## Skills Available to Agent

The agent has access to:
- **pedagogy**: General teaching principles for data science
- **content-templates**: Template structures and patterns
- **courses/bana-4080**: BANA 4080 course profile and standards
- **courses/bana-6043**: BANA 6043 course profile
- **courses/bana-7075**: BANA 7075 course profile

## Output

A complete markdown file ready for Canvas with:
- Professional module overview with business context
- Clear, measurable learning objectives (5-8 items)
- Concise "What You'll Learn" summary
- Detailed descriptions of Tuesday and Thursday activities
- Supplemental files section (TBD or populated)
- Consistent formatting and structure
- User-reviewed and approved content
- No template comments or guidance text

The overview should be immediately usable in Canvas with minimal additional editing.
