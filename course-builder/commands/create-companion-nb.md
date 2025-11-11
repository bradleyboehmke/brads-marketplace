---
description: Create a companion Jupyter notebook for a textbook chapter
---

# Create Companion Notebook

Generate a Jupyter notebook that accompanies a textbook chapter, allowing students to explore concepts interactively.

## Process

1. **Invoke the course-architect agent** to create the notebook
2. The agent will:
   - Ask which course this notebook is for
   - Load the appropriate course profile
   - Ask what chapter or topic this accompanies
   - Generate a notebook that:
     - Follows the chapter's structure
     - Includes executable code examples
     - Uses course-appropriate libraries
     - Provides interactive explorations
     - Includes exercises for students to complete

## What the Agent Does

The course-architect will:
- Create code cells with working examples from the chapter
- Add markdown cells explaining concepts
- Include visualizations to build intuition
- Design exercises that build on examples
- Use the technical stack specified in the course profile
- Match the complexity to student level

The agent has access to skills for:
- **pedagogy**: Interactive learning principles
- **content-templates**: Notebook structure patterns
- **courses/{course-name}**: Course-specific tools and libraries

## Output

A complete Jupyter notebook (.ipynb format) including:
- Markdown cells with explanations
- Code cells with working examples
- Visualizations and interactive elements
- Student exercises (with solutions in comments or separate cells)
- Clear instructions and learning objectives
- Proper imports and setup
