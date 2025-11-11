---
description: Create a lab assignment Jupyter notebook
---

# Create Lab Notebook

Generate a Jupyter notebook for a hands-on lab assignment where students apply concepts to solve problems.

## Interactive Workflow

This command uses a numbered-option interactive workflow to gather requirements and create the lab notebook.

### Step 1: Course Selection

Ask the user which course this lab is for:

```
Which course is this lab for?

[1] BANA 4080 (Intro to Data Mining - Undergraduate)
[2] BANA 6043 (Statistical Computing - Graduate)
[3] BANA 7075 (ML in Business - Graduate)

Please select an option by number:
```

**Course Mappings:**
- BANA 4080 → `bana-4080` profile (inherits from `intro-to-data-mining`) - Undergraduate
- BANA 6043 → `bana-6043` profile (inherits from `statistical-computing`) - Graduate
- BANA 7075 → `bana-7075` profile (inherits from `ml-in-business`) - Graduate

Load the appropriate course profile and, for BANA 4080, also load the `lab-template-guide` skill.

### Step 2: Chapter Input

Ask which chapters the lab should reinforce:

```
Which chapters should this lab reinforce?
(Provide chapter numbers or names, e.g., "Chapters 7-9" or "Control Flow, Functions")
```

Read the specified chapters if available to analyze content.

### Step 3: Topic Confirmation

Based on the chapters, analyze and present planned topics:

```
Based on [chapters specified], I plan to cover these topics:
- [Topic 1 identified from chapter analysis]
- [Topic 2 identified from chapter analysis]
- [Topic 3 identified from chapter analysis]
[- Additional topics as appropriate]

[1] Accept these topics
[2] Add or modify topics

Please select an option:
```

If option [2], ask:
```
Please specify additional topics to include or modifications:
```

### Step 4: Dataset Strategy

Present the dataset plan and ask for confirmation:

```
Dataset plan:
- Part A (guided reinforcement): [Primary dataset from chapter readings]
- Part B (independent challenges): [Dataset from end-of-chapter exercises]

[1] Accept these datasets
[2] Specify alternative datasets

Please select an option:
```

If option [2], ask:
```
Please specify which datasets to use:
- Part A dataset:
- Part B dataset:
```

### Step 5: Week Number

Ask what week this lab is for:

```
What week number is this lab for?
(Used for filename: XX_wkX_lab.ipynb)
```

### Step 6: Save Location

Detect if a `lab/` or `labs/` directory exists in the current working directory or nearby. Present options:

```
Where should I save the lab notebook?

[Suggested path: /path/to/lab/]

Please provide the directory path (or press Enter to use suggested path):
```

### Step 7: Generate Lab

**For BANA 4080 labs:**
1. Read the template file at `/Users/b294776/Desktop/UC/uc-bana-4080/planning/templates/lab_notebook_template.ipynb`
2. Follow the structure exactly as defined in the template
3. Replace all `[PLACEHOLDERS]` with appropriate content based on:
   - Chapters/readings specified
   - Topics confirmed
   - Datasets selected
   - Week number
   - Course profile and lab-template-guide
4. Ensure the 75-minute structure:
   - Part A: ~30 minutes of guided reinforcement
   - Class Q&A: ~5-10 minutes
   - Part B: ~35-40 minutes of independent challenges (6 challenges)
   - Wrap-up: ~3-5 minutes
5. Include:
   - Clear learning objectives (3-4 items)
   - Business context for all concepts
   - Step-by-step instructions for Part A
   - Progressive challenges for Part B (no starter code, no AI)
   - Reflection questions
   - Troubleshooting section
6. Save as `XX_wkX_lab.ipynb` in specified directory

**For BANA 6043 and 7075 labs:**
1. Use the general lab template structure from `content-templates/templates.md`
2. Adapt to graduate level and course-specific context
3. Follow course profile standards
4. Save in specified directory

### Step 8: Completion Message

Display success message with reminder about TA guide:

```
✅ Lab notebook created successfully!

Location: [full path to created file]

Next steps:
1. Review the lab notebook and make any necessary edits
2. When ready, use `/course-builder:create-ta-guide` to create the TA guidance notebook

The TA guidance notebook will include:
- Complete solutions for all challenges
- Teaching guidance for Part A sections
- Common student difficulties and hints
- Timing and facilitation strategies
```

## What the Agent Does

The course-architect agent will:

**Planning Phase:**
- Load appropriate course profile based on selection
- For BANA 4080: Load lab-template-guide skill
- Analyze specified chapters to extract key concepts
- Identify topics requiring hands-on practice
- Determine appropriate datasets from chapter content
- Confirm all details with user using numbered options

**Content Creation Phase:**
- For BANA 4080: Read and use the actual template file
- Generate lab following the exact structure required
- Fill all placeholders with specific, contextual content
- Create Part A with guided examples and "Your Turn" exercises
- Create Part B with 6 progressive business-focused challenges
- Include appropriate scaffolding for student level
- Add business context to every concept and exercise
- Ensure timing estimates are realistic

**Quality Assurance:**
- Verify all placeholders are replaced
- Ensure learning objectives align with activities
- Confirm business context is present throughout
- Validate structure matches template requirements
- Check that timing adds up to 75 minutes (for BANA 4080)

## Course-Specific Requirements

### BANA 4080 (Undergraduate)
- **Template:** Must use the provided template file exactly
- **Structure:** Part A (30 min) + Q&A (5-10 min) + Part B (35-40 min) + Wrap-up (3-5 min)
- **Part A:** Guided reinforcement with TA leading students
- **Part B:** 6 independent group challenges with NO starter code, NO AI tools
- **Tone:** Encouraging, accessible, builds confidence
- **Examples:** Relatable business scenarios for beginners
- **TA Guide Required:** Yes, created separately with `/course-builder:create-ta-guide`

### BANA 6043 & 7075 (Graduate)
- **Structure:** Flexible based on course needs
- **Tone:** More formal, assumes stronger technical background
- **Examples:** Advanced business applications, research scenarios
- **Complexity:** Higher mathematical rigor and conceptual depth
- **TA Guide:** Optional, based on instructor preference

## Skills Available to Agent

The agent has access to:
- **pedagogy**: General teaching principles for data science
- **content-templates**: Lab notebook structure patterns
- **courses/bana-4080**: BANA 4080 course profile and lab-template-guide
- **courses/bana-6043**: BANA 6043 course profile
- **courses/bana-7075**: BANA 7075 course profile
- **courses/intro-to-data-mining**: Base profile for BANA 4080
- **courses/statistical-computing**: Base profile for BANA 6043
- **courses/ml-in-business**: Base profile for BANA 7075

## Output

A complete Jupyter notebook (.ipynb format) including:
- Professional header with learning objectives
- Setup and data loading
- Guided learning sections (Part A for BANA 4080)
- Independent practice/challenges (Part B for BANA 4080)
- Business context throughout
- Reflection and wrap-up
- Troubleshooting section
- Appropriate complexity for student level
- Realistic time estimates

**Note:** The TA guidance notebook is created separately using the `/course-builder:create-ta-guide` command after the instructor reviews and approves the student lab notebook.
