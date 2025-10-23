---
description: Create TA guidance notebook with solutions and teaching strategies
---

# Create TA Guidance Notebook

Generate a comprehensive TA guidance notebook that provides complete solutions, teaching strategies, and facilitation guidance for a student lab notebook.

## Interactive Workflow

### Step 1: Locate Student Lab

Ask for the path to the student lab notebook:

```
Please provide the path to the student lab notebook:
(e.g., /path/to/labs/06_wk6_lab.ipynb)
```

Read the student lab notebook to analyze its structure and content.

### Step 2: Identify Course

Based on the lab structure or ask the user:

```
Which course is this TA guide for?

[1] BANA 4080 (Intro to Data Mining - Undergraduate)
[2] BANA 6043 (Statistical Computing - Graduate)
[3] BANA 7075 (ML in Business - Graduate)

Please select an option by number:
```

Load the appropriate course profile.

### Step 3: Extract Week Number

Extract the week number from the filename (e.g., `06_wk6_lab.ipynb` → week 6) or ask:

```
What week is this lab for?
(Used for filename: ta_guidance_wkX.ipynb)
```

### Step 4: Generate TA Guide

Create a comprehensive TA guidance notebook with:

**Section 1: Pre-Lab Preparation**
- Overview of learning objectives
- Key concepts from the lab
- Connection to readings/lectures
- Required setup and materials
- Common technical issues to anticipate
- Grouping strategies (for BANA 4080)

**Section 2: Part A Teaching Guidance** (for BANA 4080)
For each section in Part A:
- Teaching objectives for the section
- Time allocation
- Key points to emphasize
- Demonstration strategies
- Common student questions and suggested answers
- Transition techniques to next section

**Section 3: Part B Solutions and Facilitation** (for BANA 4080)
For each of the 6 challenges:
- Challenge overview and learning goal
- Complete, well-commented solution code
- Alternative approaches students might take
- Common errors and debugging strategies
- Hints to provide (when and how)
- Discussion points for concept reinforcement
- Extension ideas for advanced students

**Section 4: Timing and Pacing Strategies**
- Detailed timing breakdown
- What to do if running ahead/behind
- How to manage different group paces
- When to call class back together
- Transition management

**Section 5: Assessment and Wrap-up**
- Key concepts students should have mastered
- Reflection questions to ask
- Connections to upcoming content/homework
- What to look for when monitoring student work

**Section 6: Troubleshooting Guide**
- Common technical issues and solutions
- Conceptual difficulties and how to address
- Group dynamics issues
- Backup plans for major problems

### Step 5: Save Location

Suggest saving in the same directory as the student lab:

```
Where should I save the TA guidance notebook?

[Suggested: same directory as student lab]

Please provide the directory path (or press Enter to use suggested path):
```

Save as `ta_guidance_wkX.ipynb`

### Step 6: Completion Message

```
✅ TA guidance notebook created successfully!

Location: [full path to created file]

The TA guidance includes:
- Pre-lab preparation guidance
- Part A teaching strategies (section-by-section)
- Part B complete solutions (all challenges)
- Timing and pacing strategies
- Troubleshooting guide

Review the guidance and customize as needed for your teaching style.
```

## What the Agent Does

The course-architect agent will:

**Analysis Phase:**
- Read and analyze the student lab notebook
- Identify all exercises, challenges, and learning objectives
- Extract the lab structure (Part A sections, Part B challenges)
- Load appropriate course profile

**Solution Development:**
- Create complete, tested solutions for all challenges
- Write well-commented code explaining each step
- Identify alternative valid approaches
- Document common errors and misconceptions

**Teaching Guidance Creation:**
- Develop section-by-section teaching strategies for Part A
- Provide timing guidance and pacing strategies
- Suggest when and how to provide hints
- Create discussion prompts and check-in questions

**Quality Assurance:**
- Ensure all solutions are complete and tested
- Verify timing estimates are realistic
- Confirm guidance covers common student difficulties
- Check that facilitation strategies are practical

## Course-Specific Requirements

### BANA 4080 (Undergraduate)

**Structure:** Must include all sections listed above

**Part A Guidance Should Include:**
- Step-by-step teaching script for each section
- What to write/show on screen
- Questions to ask students to check understanding
- How to explain concepts in accessible language
- When to have students try on their own

**Part B Solutions Should Include:**
- Complete working code for all 6 challenges
- Multiple approaches where applicable
- Common mistakes students make
- Strategic hints (not full solutions) to provide
- When to intervene vs. let groups struggle productively
- Discussion points after each challenge

**Timing Guidance:**
- Detailed breakdown matching the 75-minute structure
- Flexibility strategies for different pacing
- What to skip if running behind
- Extension activities if running ahead

### BANA 6043 & 7075 (Graduate)

**Structure:** More flexible, focus on:
- Complete solutions to all exercises
- Advanced discussion topics
- Connections to research or industry applications
- Optional: Teaching strategies if lab is TA-led

## Output

A comprehensive Jupyter notebook (.ipynb format) including:
- Complete solutions to all lab exercises and challenges
- Teaching strategies for guided sections
- Timing and pacing guidance
- Common student difficulties and how to address them
- Facilitation strategies for group work
- Troubleshooting guide
- Discussion prompts and assessment questions

The TA guide should be a complete resource that allows a TA to effectively facilitate the lab session even if they haven't taught it before.
