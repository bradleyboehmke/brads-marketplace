---
description: Create presentation slides for a lecture
---

# Create Slides

Generate presentation slides for teaching a course topic using the Quarto RevealJS format.

## Interactive Workflow

This command uses a numbered-option interactive workflow to gather requirements and create lecture slides.

### Step 1: Course Selection

Ask the user which course these slides are for:

```
Which course are these slides for?

[1] BANA 4080 (Intro to Data Mining - Undergraduate)
[2] BANA 6043 (Statistical Computing - Graduate)
[3] BANA 7075 (ML in Business - Graduate)

Please select an option by number:
```

Load the appropriate course profile.

### Step 2: Chapter Input

Ask which chapters the slides should cover:

```
Which chapters should these slides cover?
(Provide chapter numbers or names, e.g., "Chapters 7-9" or "Control Flow, Functions")
```

Read the specified chapters if available to analyze content and extract key concepts.

### Step 3: Week Number

Ask what week these slides are for:

```
What week number are these slides for?
(Used for filename: w[X]_tuesday.qmd)
```

### Step 4: Dataset Confirmation

Present the dataset plan:

```
Dataset plan for demonstrations:
I'll use the primary dataset from the chapter readings for live coding examples.

[1] Accept this dataset
[2] Specify a different dataset

Please select an option:
```

If option [2], ask:
```
Please specify which dataset to use for demonstrations:
```

### Step 5: Present Slide Outline

Analyze the chapters and present a proposed outline:

```
Based on [chapters specified], here's the proposed slide outline:

Opening & Agenda (5 minutes)
├── Week overview and learning objectives
└── Connection to course progression

Review & Warm-Up (10-15 minutes)
├── Previous week concept review
└── Think-pair-share connection activity

Main Content (35-45 minutes)
├── [Concept 1 Title]
│   └── Interactive Activity: [Activity description]
├── [Concept 2 Title]
│   └── Hands-On Demo: [Demo description]
└── [Concept 3 Title]
    └── Interactive Activity: [Activity description]

Wrap-Up (10-15 minutes)
├── Key takeaways
├── Thursday lab preview
└── Q&A

[1] Accept this outline and generate slides
[2] Request changes to outline

Please select an option:
```

If option [2], ask:
```
What changes would you like to make to the outline?
```

Then regenerate the outline and present again.

### Step 6: Save Location

When user accepts the outline, ask where to save:

```
Where should I save the slides?

[Suggested: Look for slides/ directory or current working directory]

Please provide the directory path (or press Enter to use suggested path):
```

### Step 7: Generate Slides

**For BANA 4080 slides:**
1. Read the template file at `/Users/b294776/Desktop/UC/uc-bana-4080/planning/templates/tuesday_slide_template.qmd`
2. Follow the structure exactly as defined in the template
3. Replace all `[PLACEHOLDERS]` with appropriate content based on:
   - Chapters/readings specified
   - Week number
   - Dataset selected
   - Course profile requirements
4. Create interactive think-pair-share activities (3-4 minimum)
5. Include hands-on demonstrations with business context
6. Add appropriate timers with unique IDs
7. Generate visualizations using Mermaid diagrams or Python code where applicable
8. Save as `w[X]_tuesday.qmd` in specified directory

**For BANA 6043 and 7075 slides:**
1. Use general slide template structure from `content-templates/templates.md`
2. Adapt to graduate level and course-specific context
3. Follow course profile standards
4. Save in specified directory

### Step 8: Post-Generation Notes

After saving the slides, provide notes about elements requiring attention:

```
✅ Slides created successfully!

Location: [full path to created file]

📋 Action Items:
The following elements may need your attention:

Images Needed:
- [List any image placeholders with slide numbers]
- Suggested sources: Create with Mermaid, generate with Python, or source from [suggestions]

Visualizations Created:
- [List Mermaid diagrams or Python-generated visualizations included]

Custom Content:
- [Any sections that may need customization based on specific context]

Next steps:
1. Review the slides in your editor
2. Add or create any required images
3. Test render the .qmd file to HTML
4. Review interactive elements and timers
```

## What the Agent Does

The course-architect agent will:

**Analysis Phase:**
- Load appropriate course profile based on selection
- Read and analyze specified chapters to extract key concepts
- Identify 3-4 core concepts for gentle introduction
- Map business applications and real-world relevance
- Plan hands-on demonstration opportunities

**Outline Design Phase:**
- Design 3-4 think-pair-share activities with business scenarios
- Create 1-2 hands-on demonstrations for immediate success
- Develop progressive concept flow from familiar to sophisticated
- Plan Thursday lab connections and motivation
- Present outline for user approval

**Content Generation Phase:**
- For BANA 4080: Read and use the actual template file
- Generate slides following the exact structure required
- Fill all placeholders with specific, contextual content
- Create business scenarios that students find relatable
- Develop code demonstrations (using chapter datasets)
- Design timer activities with unique IDs
- **Prefer Mermaid diagrams or Python-generated visualizations** over external images
- Add speaker notes for instructor guidance

**Quality Assurance:**
- Verify all placeholders are replaced
- Ensure 3-4 interactive activities included
- Confirm business context is present throughout
- Validate structure matches template requirements
- Check that timing adds up to 60-75 minutes
- Note any image placeholders that need attention

## Course-Specific Requirements

### BANA 4080 (Undergraduate)
- **Template:** Must use the provided template file exactly
- **Duration:** 60-75 minutes total
- **Structure:** Opening (5 min) + Review (10-15 min) + Main Content (35-45 min) + Wrap-Up (10-15 min)
- **Interactive Activities:** Minimum 3-4 think-pair-share activities with timers
- **Hands-On Demos:** 1-2 live coding demonstrations using chapter datasets
- **Tone:** Gentle introduction, business-focused, success-oriented
- **Philosophy:** First exposure to concepts before readings and Thursday lab
- **Visualizations:** Prefer Mermaid diagrams and Python-generated charts

### BANA 6043 & 7075 (Graduate)
- **Structure:** Flexible based on course needs
- **Tone:** More formal, assumes stronger technical background
- **Examples:** Advanced business applications, research scenarios
- **Complexity:** Higher mathematical rigor and conceptual depth

## Skills Available to Agent

The agent has access to:
- **pedagogy**: Presentation and lecture design principles, gentle introduction strategies
- **content-templates**: Slide structure patterns
- **courses/bana-4080**: BANA 4080 course profile and standards
- **courses/bana-6043**: BANA 6043 course profile
- **courses/bana-7075**: BANA 7075 course profile

## Output

A complete Quarto RevealJS presentation (.qmd format) including:
- YAML header with RevealJS configuration
- Professional title slide with background image
- Opening and agenda slides
- Previous week review section with interactive activity
- Main content sections with business context
- Interactive think-pair-share activities with timers
- Hands-on demonstrations with code
- Mermaid diagrams or Python-generated visualizations (preferred over external images)
- Key takeaways and Thursday lab preview
- Wrap-up and Q&A slides
- Speaker notes for instructor guidance
- Appropriate complexity for student level
- Realistic time estimates (60-75 minutes total)

**Post-Generation Notes:** The agent will provide a list of any image placeholders, visualization elements created, and items requiring instructor attention before finalizing the slides.
