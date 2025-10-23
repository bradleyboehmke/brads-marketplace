---
description: Create a lab assignment Jupyter notebook
---

# Create Lab Notebook

Generate a Jupyter notebook for a hands-on lab assignment where students apply concepts to solve problems.

## Process

1. **Invoke the course-architect agent** to create the lab
2. The agent will:
   - Ask which course this lab is for
   - Load the appropriate course profile
   - Ask what concepts/skills the lab should practice
   - Ask for lab parameters (difficulty, time estimate, scaffolding level)
   - Generate a lab notebook that:
     - Presents a real-world problem or dataset
     - Guides students through analysis steps
     - Provides scaffolding appropriate to student level
     - Includes checkpoints and validation
     - Encourages exploration and experimentation

## What the Agent Does

The course-architect will:
- Design a problem that applies course concepts
- Provide a realistic dataset (or instructions to generate one)
- Create starter code with TODOs for students to complete
- Include hints and guidance at appropriate levels
- Add validation cells to check student work
- Match complexity and tools to the course profile

The agent has access to skills for:
- **pedagogy**: Lab design and scaffolding principles
- **content-templates**: Lab notebook patterns
- **courses/{course-name}**: Course-specific skills and tools

## Output

A complete Jupyter notebook (.ipynb format) including:
- Problem statement and context
- Dataset and/or data generation code
- Starter code with clear TODOs
- Markdown cells with instructions and guidance
- Validation/check cells
- Optional: Solution notebook
- Learning objectives and expected time
