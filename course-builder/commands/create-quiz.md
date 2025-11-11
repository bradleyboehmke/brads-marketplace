---
description: Create a reading comprehension quiz based on chapter content
---

# Create Quiz

Generate a reading comprehension quiz to test student understanding of textbook chapter(s).

## Purpose

Creates "reading quizzes" that verify students comprehended key concepts from assigned chapter readings. These quizzes focus on understanding, not memorization, and use business scenarios to bring concepts to life.

## Process

1. **Invoke the course-architect agent** to create the quiz
2. The agent will:
   - Ask which course this quiz is for
   - Load the appropriate course profile
   - **Ask which chapter(s) to base the quiz on** (e.g., "Chapter 5: Data Visualization")
   - **Confirm the number of questions** (default: 10 questions, but allow customization)
   - **Ask for the week number** (e.g., "Week 9") for filename generation
   - **Ask where to save the quiz** (provide default based on course, allow customization)
   - Read the specified chapter(s) to understand content and learning objectives
   - Generate quiz questions that:
     - Test comprehension of key concepts from the reading
     - Include business scenario-based questions
     - Use appropriate question types (multiple choice, true/false, multiple answer, numeric entry)
     - Match the course's pedagogical style
   - **Save the quiz** as a markdown file to the specified location

## Quiz Structure

Each quiz question must include:

1. **Question Number and Title** (e.g., "Question 3: Linear Regression Coefficients")
2. **Question Type** (Multiple Choice, TRUE/FALSE, Multiple Answer, or Numeric Entry)
3. **Scenario** (for scenario-based questions) - Business context that applies the concept
4. **Question** - Clear, specific question text
5. **Answer Options** - Varies by question type:
   - Multiple Choice: 4 options (A, B, C, D)
   - TRUE/FALSE: 2 options (A: TRUE, B: FALSE)
   - Multiple Answer: 4-5 options with instruction to "Select ALL correct"
   - Numeric Entry: Blank for student to fill in, with acceptable answer range/precision
6. **Correct Answer** - Clearly identified with precision requirements for numeric entries
7. **Tip/Hint** - Helpful guidance for wrong answers that:
   - Doesn't give away the answer
   - Points to the key concept they need to reconsider
   - Helps them think through the problem
   - References relevant parts of the reading
   - For numeric questions: points to the calculation method or formula needed

## Question Types Distribution

For a typical 10-question quiz:
- **5-6 Multiple Choice** questions (standard comprehension + scenario-based)
- **2-3 TRUE/FALSE** questions (test common misconceptions)
- **1-2 Multiple Answer** questions (select ALL correct - tests nuanced understanding)
- **0-2 Numeric Entry** questions (test calculation/application skills)

**Important:** Mix scenario-based questions throughout. At least 40-50% of questions should use business scenarios.

## What the Agent Does

The course-architect will:
- Read the specified chapter(s) to extract key concepts and learning objectives
- Create questions that test understanding, not just recall
- Write realistic business scenarios that apply the concepts
- Ensure questions match the course's student level and style
- Provide helpful tips that guide thinking without revealing answers
- Balance question types and difficulty
- Avoid questions that are too easy (pure recall) or too trick-y

The agent has access to skills for:
- **pedagogy**: Assessment design principles (test understanding, not memorization)
- **content-templates**: Quiz format templates
- **courses/{course-name}**: Course-specific context, student level, and learning philosophy

## Output Format

A complete quiz markdown file including:

```markdown
# Week [X] Quiz: [Topic Name]

**Instructions:** This quiz tests your comprehension of Week [X] material including [key topics]. Choose the best answer(s) for each question.

---

## Question 1: [Concept Name] ([Question Type])

**Scenario:** [Business scenario if applicable]

[Question text]

A) [Option A]
B) [Option B]
C) [Option C]
D) [Option D]

**Correct Answer:** [Letter]

**Tip for wrong answers:** [Helpful guidance that doesn't reveal the answer]

---

[Repeat for remaining questions]
```

## Example Question Patterns

**Scenario-Based Multiple Choice:**
```
## Question 5: Model Evaluation (Multiple Choice)

**Scenario:** A retail analytics team builds a sales forecasting model.
Training RMSE is $450, but Test RMSE is $1,200.

What does this suggest?
A) The model is ready for deployment
B) The model is overfitting
C) The model is underfitting
D) The test data is bad

**Correct Answer:** B

**Tip:** Consider what a large gap between training and test performance indicates about how well the model generalizes to new data.
```

**Concept Application TRUE/FALSE:**
```
## Question 2: Correlation vs. Causation (TRUE/FALSE)

**Statement:** If advertising spend and sales have correlation 0.85,
we can conclude advertising causes sales increases.

A) TRUE
B) FALSE

**Correct Answer:** B

**Tip:** Remember that correlation measures association, not causation.
What other factors might explain both variables moving together?
```

**Numeric Entry:**
```
## Question 8: Calculate Correlation (Numeric Entry)

**Scenario:** A marketing analyst calculates the covariance between
advertising spend and sales as 1,200. The standard deviation of
advertising spend is 30 and the standard deviation of sales is 50.

What is the correlation coefficient? (Round to 2 decimal places)

Answer: ______

**Correct Answer:** 0.80

**Acceptable Range:** 0.79 to 0.81

**Tip:** Remember the formula: correlation = covariance / (SD of X × SD of Y).
Make sure you're dividing, not multiplying the standard deviations.
```

**Multiple Answer:**
```
## Question 10: Regression Assumptions (Multiple Answer - Select ALL correct)

Which of these are key assumptions of linear regression?

A) The relationship between predictors and outcome is linear
B) The residuals (errors) are normally distributed
C) All predictor variables must be normally distributed
D) The variance of residuals is constant
E) Residuals are independent of each other

**Correct Answers:** A, B, D, E

**Tip:** Linear regression doesn't require predictor variables to be normally
distributed, only that the residuals follow a normal distribution.
```

## Save Location

The agent will ask where to save the quiz and provide a course-specific default:

**For Intro to Data Mining (BANA 4080):**
- Default: `/Users/b294776/Desktop/UC/uc-bana-4080/planning/quizzes/`
- Filename format: `week[X]_quiz.md` (e.g., `week9_quiz.md`)

**For other courses:**
- The agent will suggest an appropriate location based on the course profile
- Always confirm the save location before writing the file

**After generation:**
1. Show the user the complete quiz content
2. Confirm the save location and filename
3. Use the Write tool to save the file
4. Confirm successful save to the user

## Important Notes

- **Chapter-driven:** Always ask which chapter(s) to base the quiz on
- **Week number:** Ask for the week number to create proper filename
- **Confirm quantity:** Ask to confirm 10 questions (or get desired number)
- **Scenario-based:** Mix business scenarios throughout (40-50% of questions)
- **Helpful tips:** Guide thinking, don't reveal answers
- **Course-appropriate:** Match student level and course style
- **Question type variety:** Use all four types (Multiple Choice, TRUE/FALSE, Multiple Answer, Numeric Entry)
- **Numeric precision:** For numeric entry questions, always specify:
  - Required precision (e.g., "rounded to 1 decimal place")
  - Acceptable answer range to account for rounding differences
  - Clear calculation context from the scenario
- **No coding questions:** Reading quizzes test conceptual understanding and calculations, not coding ability
- **Save workflow:** Always confirm save location and filename before writing the file
