# BANA 4080 Lab Template Guide

This guide provides the structure and requirements for creating Thursday lab notebooks for BANA 4080.

## Template Location

**File:** `/Users/b294776/Desktop/UC/uc-bana-4080/planning/templates/lab_notebook_template.ipynb`
**Usage Guide:** `/Users/b294776/Desktop/UC/uc-bana-4080/planning/templates/lab_template_usage_guide.md`

## Lab Structure (75 minutes)

### Header Section
- Week number and descriptive lab title
- Colab badge with correct filename
- Lab description and context (2-3 sentences)
- **Learning Objectives:** 3-4 specific, measurable outcomes starting with action verbs
- **This Lab Reinforces:** List of chapter/reading references
- **Estimated Time & Structure:** Clear breakdown with realistic time estimates
- **Why This Matters:** Business context and real-world relevance

### Setup Section
- Required imports (only necessary libraries)
- Data loading code
- Quick preview/verification of loaded data

### Part A: Guided Reinforcement (~30 minutes)

**Part 1** — [Section 1 Title] (Time estimate)
- Section description and context
- Subsection with explanation/instructions
- Step-by-step instructions (numbered)
- Code examples or starter code
- "🧠 Your Turn" exercise with tasks
- Empty code cell for practice
- "✅ Check Your Understanding" with questions and expected results

**Part 2** — [Section 2 Title] (Time estimate)
- Similar structure to Part 1
- Guided example with explanation
- Demonstration code
- "🧪 Practice Exercise" with business scenario
- Step-by-step approach
- Code cell for solution

**Class Discussion/Q&A** (5-10 minutes)
- Discussion prompts
- Common blockers and clarifications

### Part B: Independent Group Challenges (~35-40 minutes)

**Intro markdown:**
```markdown
For the next several challenges:
* You will not be given starter code
* **DO NOT USE AI** to generate code
* Work in groups of 2-4 students
* Feel free to ask questions or seek help from instructor
* We'll stop and walk through each challenge together after each time block
```

**Challenge 1** — [Title] (6-8 minutes)
- Business question
- Additional context if needed
- Empty code cell with comment: `# Your turn: write code here to [description]`

**Challenge 2** — [Title] (6-8 minutes)
- Business question
- Strategic hint (not code)
- Empty code cell

**Challenge 3-6** — Similar structure with progressive difficulty

### Optional Extension Activities

**Extension 1-2:** Advanced challenges for early finishers
**Extension 3:** "Brainstorm - What else is interesting?" with example questions

### Lab Wrap-Up & Reflection (3-5 minutes)

- **What You Accomplished:** List of accomplishments
- **Reflection Questions:** 2-3 metacognitive prompts
- **Connection to Course Goals:** How this lab connects to broader learning
- **Next Steps:** Homework reference, next week preview, optional resources
- Save your work instruction

### Troubleshooting & Common Issues

- Issue 1-3 with solutions
- General debugging tips

## Required Placeholders to Fill

All items in `[BRACKETS]` must be replaced:

| Placeholder | Example |
|-------------|---------|
| `[X]` | Week number (e.g., `6`) |
| `[LAB_TITLE]` | `Control Flow and Functions in Practice` |
| `[FILENAME]` | `06_wk6_lab` |
| `[LAB_DESCRIPTION_AND_CONTEXT]` | Description of what students will do |
| `[OBJECTIVE_1]` | `Write conditional statements for business logic` |
| `[Reading/Chapter Reference 1]` | `Chapter 7: Control Flow` |
| `[TIME_ESTIMATE]` | `15-20` |
| `[BUSINESS_CONTEXT_AND_REAL_WORLD_RELEVANCE]` | Why this matters in real work |
| `[SECTION_X_TITLE]` | Name of major section |
| `[SUBSECTION_X_TITLE]` | Name of subsection |
| `[EXPLANATION_OR_INSTRUCTIONS]` | Teaching content |
| `[STEP_X]` | Individual step in process |
| `[DESCRIPTIVE_COMMENT]` | What the code does |
| `[CODE_EXAMPLE_OR_STARTER]` | Actual code |
| `[EXERCISE_TITLE]` | Name of practice exercise |
| `[EXERCISE_DESCRIPTION]` | What students should do |
| `[TASK_X]` | Individual task |
| `[HELPFUL_HINT_IF_NEEDED]` | Strategic guidance |
| `[MINI_ASSESSMENT_OR_DISCUSSION_QUESTIONS]` | Comprehension check |
| `[QUESTION_X]` | Specific question |
| `[WHAT_STUDENTS_SHOULD_SEE]` | Expected output/result |
| `[CONCRETE_BUSINESS_EXAMPLE]` | Real scenario |
| `[DEMONSTRATION_CODE]` | Working example |
| `[REALISTIC_BUSINESS_CONTEXT]` | Business scenario for exercise |
| `[CLEAR_TASK_DESCRIPTION]` | What to accomplish |
| `[CHALLENGE_TITLE]` | Name of challenge |
| `[BUSINESS_QUESTION]` | Question to answer |
| `[ADDITIONAL_CONTEXT_IF_NEEDED]` | Extra info |
| `[CHALLENGE_DESCRIPTION]` | What the code should do |
| `[STRATEGIC_HINT_NOT_CODE]` | Approach guidance |
| `[EXTENSION_TITLE]` | Name of extension |
| `[ADVANCED_CHALLENGE_DESCRIPTION]` | Extension task |
| `[EXAMPLE_QUESTION_X]` | Sample brainstorm question |
| `[ACCOMPLISHMENT_X]` | What was learned |
| `[HOW_THIS_LAB_CONNECTS_TO_BROADER_LEARNING]` | Big picture |
| `[HOMEWORK_REFERENCE]` | Link to assignment |
| `[NEXT_WEEK_PREVIEW]` | What's coming |
| `[OPTIONAL_RESOURCES]` | Additional materials |
| `[SPECIFIC_SHARING_INSTRUCTIONS]` | How to share work |
| `[COMMON_PROBLEM]` | Issue students face |
| `[SOLUTION_APPROACH]` | How to fix |
| `[TIP_X]` | Debugging tip |

## Content Development Process

### Phase 1: Content Analysis
1. Review assigned chapter(s) for the week
2. Identify key concepts that need hands-on practice
3. Map concepts to Part A (guided) and Part B (challenges)
4. Define 3-4 specific learning objectives

### Phase 2: Part A Design (Guided Reinforcement)
- Systematically review key concepts from readings
- Provide hands-on practice with instructor guidance
- Include "Your Turn" exercises for immediate application
- Build confidence before independent work

**Principles:**
- Students follow along and execute code together
- Explain rationale and connect to business applications
- Multiple opportunities for questions
- Gradual release of responsibility

### Phase 3: Part B Design (Independent Challenges)
- Create 6 challenges with progressive difficulty
- Each challenge: clear business question, minimal code scaffolding
- Strategic hints rather than direct solutions
- Require integration of multiple concepts

**Principles:**
- Groups work collaboratively with minimal intervention
- Business context makes problems meaningful
- Different groups can progress at different paces
- No AI tools allowed - students write code themselves

### Phase 4: Dataset Selection
**Default Strategy:**
- Part A (guided): Primary dataset from chapter readings
- Part B (challenges): Dataset from end-of-chapter exercises
- Always confirm with instructor and allow alternatives

### Phase 5: Quality Validation
- [ ] All code tested in Google Colab
- [ ] Chapter alignment verified
- [ ] 75-minute timing realistic
- [ ] Part A/B balance appropriate (~30 min / ~35-40 min)
- [ ] Business context realistic
- [ ] Learning objectives align with activities
- [ ] All placeholders replaced
- [ ] Colab badge updated

## TA Guidance Requirements

Each lab requires a companion `ta_guidance_wkX.ipynb` with:

**Pre-Lab Preparation:**
- Learning objectives and key concepts overview
- Connection to readings
- Setup instructions and common issues
- Classroom management tips

**Part A Teaching Guidance:**
- Section-by-section instructions with timing
- Key concepts to emphasize
- Common student questions and responses
- Teaching strategies

**Part B Facilitation Guide:**
- Complete solutions for all 6 challenges
- Common difficulties and targeted hints
- When and how to provide assistance
- Pacing strategies

**Assessment and Wrap-up:**
- Key concepts to verify mastery
- Reflection questions
- Connection to upcoming content
- Troubleshooting guide

## Business Context Standards

Every concept and exercise must have clear business relevance:
- Real-world scenarios students can relate to
- Authentic business questions and problems
- Professional applications and use cases
- Connection to career skills

**Good examples:**
- Customer segmentation analysis
- Marketing campaign performance
- Retail transaction patterns
- Product recommendation systems
- Sales forecasting

**Avoid:**
- Abstract mathematical exercises without context
- Toy problems with no real-world connection
- Examples that don't relate to business analytics

## Common Lab Types by Week

**Weeks 1-3 (Fundamentals):**
- More guided examples, slower pacing
- Simple, clear-cut problems
- Accessible business scenarios
- Building basic confidence

**Weeks 4-6 (Skill Application):**
- Less guidance, more problem-solving
- Multi-step business problems
- Realistic data analysis scenarios
- Integration of concepts

**Weeks 7+ (Advanced Integration):**
- Open-ended exploration
- Complex, multi-faceted problems
- Comprehensive case studies
- Professional-level analysis

## Remember

- Labs directly reinforce Tuesday lecture concepts
- Based on weekly assigned chapter readings
- 75 minutes exactly with strategic time allocation
- Two-part structure: guided (30 min) + independent (35-40 min)
- Business context for everything
- No AI tools in Part B challenges
- Always create companion TA guidance notebook
