---
description: Create presentation slides for a lecture
---

# Create Slides

Generate presentation slides for teaching a course topic.

## Process

1. **Invoke the course-architect agent** to create the slides
2. The agent will:
   - Ask which course these slides are for
   - Load the appropriate course profile
   - Ask what topic the lecture covers
   - Ask for presentation parameters (length, detail level, format preference)
   - Generate slides that:
     - Present concepts in a logical flow
     - Include visual aids and examples
     - Match the student level and course style
     - Support active learning during lecture
     - Provide speaker notes

## What the Agent Does

The course-architect will:
- Structure slides for effective teaching flow
- Include visual diagrams and code examples
- Balance text with visuals
- Add speaker notes with teaching tips
- Match complexity to student level
- Use course-appropriate examples and tools

The agent has access to skills for:
- **pedagogy**: Presentation and lecture design principles
- **content-templates**: Slide structure patterns
- **courses/{course-name}**: Course-specific content style

## Output

Presentation slides in markdown format (can be converted to reveal.js, PowerPoint, etc.) including:
- Title and learning objectives
- Concept slides with clear explanations
- Visual diagrams and examples
- Code snippets (if applicable)
- Practice problems or discussion prompts
- Summary slide
- Speaker notes for each slide
