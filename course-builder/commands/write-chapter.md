---
description: Write a textbook chapter for a data science course
---

# Write Chapter

Create a textbook chapter tailored to a specific course's audience and learning objectives.

## Process

1. **Invoke the course-architect agent** to handle the chapter creation
2. The agent will:
   - Ask which course this chapter is for
   - Load the appropriate course profile
   - Ask for the chapter topic
   - Generate a chapter outline based on course standards
   - Write the complete chapter with appropriate:
     - Explanations at the right level
     - Examples using course-appropriate tools
     - Exercises and checkpoints
     - Visual aids and code snippets (if applicable)

## What the Agent Does

The course-architect will:
- Adapt writing style to the student level (undergrad vs grad)
- Use the technical stack specified in the course profile
- Follow the course's pedagogical philosophy
- Structure content according to learning objectives
- Include hands-on examples appropriate for the course

The agent has access to skills for:
- **pedagogy**: Data science teaching principles
- **content-templates**: Chapter structure templates
- **courses/{course-name}**: Course-specific context and standards

## Output

A complete markdown chapter ready to use in your textbook, including:
- Learning objectives
- Conceptual explanations
- Code examples (if applicable)
- Visualizations and diagrams
- Practice problems
- Summary and key takeaways
