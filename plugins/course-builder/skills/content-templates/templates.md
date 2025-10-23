# Content Templates

Structural templates for different types of educational content.

## Chapter Template

```markdown
# Chapter [X]: [Topic Name]

## Learning Objectives
By the end of this chapter, you will be able to:
- [Objective 1 - action verb + specific skill]
- [Objective 2]
- [Objective 3]

## Introduction
[1-2 paragraphs motivating the topic]
- Why is this important?
- What real-world problems does it solve?
- How does it connect to previous chapters?

## [Section 1: Core Concept]

### Intuition
[Explain the concept using analogies or simple examples]

### Formal Definition
[Mathematical or technical definition]

### Example
[Concrete example with code if applicable]

```python
# Code example
```

### Visualization
[Description of diagram or plot to include]

## [Section 2: Application]
[Show how to use the concept]

## [Section 3: Advanced Topics]
[Optional: deeper dive for interested students]

## Practice Problems
1. [Problem testing basic understanding]
2. [Problem requiring application]
3. [Challenge problem]

## Summary
- Key takeaway 1
- Key takeaway 2
- Key takeaway 3

## Further Reading
- [Resource 1]
- [Resource 2]
```

## Quiz Template

```markdown
# Quiz: [Topic Name]

**Instructions:** [Time limit, allowed resources, submission format]

## Part 1: Conceptual Understanding

### Question 1 (X points)
[Multiple choice, short answer, or true/false]

**Answer:** [For instructor use]

### Question 2 (X points)
[Conceptual question]

## Part 2: Application

### Question 3 (X points)
[Code-based or problem-solving question]

```python
# Starter code if applicable
```

**Expected output:** [Description]

## Part 3: Analysis

### Question 4 (X points)
[Interpretation or explanation question]

---

## Answer Key

[Detailed answers and grading rubric]

**Total Points:** XX
```

## Jupyter Notebook Template (Companion)

```markdown
# [Topic Name] - Companion Notebook

**Learning Objectives:**
- [Objective 1]
- [Objective 2]

---

## Setup
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

# Configuration
%matplotlib inline
plt.style.use('seaborn')
```

## Section 1: [Concept Name]

[Markdown explanation matching chapter]

```python
# Executable example from chapter
```

**Try it yourself:** [Suggested modifications to explore]

## Section 2: Interactive Exploration

```python
# Code for students to experiment with
```

**Questions to explore:**
1. What happens if you change X?
2. Try different values for Y
3. Visualize the results

## Section 3: Practice Exercises

### Exercise 1
[Description]

```python
# TODO: Your code here
```

**Validation:**
```python
# Check your answer
assert ..., "Check failed!"
print("✓ Correct!")
```

## Summary

[Key points reinforced in this notebook]
```

## Jupyter Notebook Template (Lab)

```markdown
# Lab [X]: [Topic Name]

**Estimated Time:** X hours
**Difficulty:** [Beginner/Intermediate/Advanced]

## Learning Objectives
- [Objective 1]
- [Objective 2]

---

## Problem Statement

[Real-world problem description]

## Dataset

[Description and source of data]

```python
# Load or generate dataset
```

**Explore the data:**
```python
# TODO: Examine the dataset
# - Check dimensions
# - Look at first few rows
# - Check for missing values
```

## Task 1: [Subtask Name]

[Instructions]

```python
# TODO: Your code here


# Solution will go here
```

**Checkpoint:** [How to verify this step]

## Task 2: [Next Subtask]

[Instructions building on Task 1]

```python
# TODO: Your code here
```

## Task 3: [Final Analysis]

[Open-ended analysis task]

## Bonus Challenge (Optional)

[Extension for advanced students]

## Reflection Questions

1. What was the most challenging part?
2. What did you learn?
3. How could you extend this analysis?
```

## Slides Template (Markdown)

```markdown
---
title: [Topic Name]
author: [Your Name]
date: [Date]
---

# [Topic Name]

## Learning Objectives

- Objective 1
- Objective 2
- Objective 3

---

## Why This Matters

[Motivation - 1-2 bullet points with visual]

**Real-world application:** [Example]

::: notes
[Speaker notes: Hook students with interesting context]
:::

---

## [Concept 1]: Intuition

[Visual diagram or simple example]

- Key point 1
- Key point 2

::: notes
[Teaching tips, common misconceptions to address]
:::

---

## [Concept 1]: Formal Definition

[Mathematical notation or technical definition]

**In plain English:** [Simplified explanation]

---

## Example: [Concrete Case]

```python
# Code example
```

**Output:**
```
[Expected output]
```

---

## Practice Problem

[Quick problem for students to try]

**Think-Pair-Share:** Discuss with your neighbor

::: notes
[Give 2-3 minutes, walk around, call on students]
:::

---

## Key Takeaways

1. [Main point 1]
2. [Main point 2]
3. [Main point 3]

**Next time:** [Preview next topic]

---

## Questions?

[Contact info or office hours]
```

## Usage Guidelines

### When to Use Each Template

- **Chapter**: Comprehensive coverage of a topic for reading/study
- **Quiz**: Assess understanding of covered material
- **Companion Notebook**: Follow along with chapter, explore interactively
- **Lab Notebook**: Apply concepts to solve realistic problems
- **Slides**: Support lecture or presentation

### Customization

These templates should be adapted based on:
- Student level (undergrad vs grad)
- Course philosophy (theory vs applied)
- Time available
- Prerequisites
- Tools and libraries used

Always reference the specific course profile for customization guidance.
