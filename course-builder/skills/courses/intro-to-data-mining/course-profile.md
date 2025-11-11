# Intro to Data Mining - Course Profile

**Course:** UC BANA 4080: Introduction to Data Mining with Python
**Instructor:** Brad Boehmke

## Audience

**Student Level:** Undergraduate (juniors/seniors)

**Background:**
- Business students with foundation in calculus, statistics, and possibly regression
- May have Excel experience and basic VBA exposure
- Variable programming backgrounds - many are complete coding beginners
- Understand business operations, customer behavior, and quantitative thinking
- Know how to think critically but lack experience turning theory into practice with code

**Prerequisites:**
- Quantitative methods and statistical inference courses
- No prior programming experience required or expected
- Course explicitly designed for beginners

**Key Challenge:** Bridging the gap between classroom theory and real-world data analysis

## Learning Philosophy

**Core Approach:** Hands-on, immersive learning through doing

**Key Principles:**
1. **Practice over theory** - Students learn by working with real, messy datasets
2. **Build confidence through action** - Focus on getting students comfortable with tools before perfection
3. **Close the theory-practice gap** - Move from "knowing concepts" to "applying skills"
4. **AI as assistant, not autopilot** - Use GenAI tools (ChatGPT, Claude, Copilot) to help learn, but emphasize understanding
5. **Collaborative learning** - Build community; encourage students to help each other
6. **Growth mindset** - Normalize struggle; coding is a new language that takes time

**Teaching Style:**
- Conversational, relatable tone (see intro chapter example)
- Use storytelling and scenarios (e.g., "Taylor the intern")
- Address student concerns directly (e.g., "Why learn this when AI exists?")
- Set realistic expectations about difficulty
- Encourage persistence and resilience

**Unique Aspects:**
- Explicitly addresses role of GenAI in learning process
- Balances AI assistance with foundational skill building
- Uses real-world business contexts students can relate to

## Technical Stack

**Core Environment:**
- **Python** (chosen for beginner-friendliness + professional power)
- **Jupyter Lab/Notebooks** (primary development environment)
- **Google Colab** (cloud-based option for students)
- **Quarto** (for textbook and slides)
- **Virtual environment** (venv for package management)

**Primary Libraries (Weeks 1-6):**
- **pandas** - data manipulation and DataFrames
- **numpy** - numerical computation
- **matplotlib** - basic visualization
- **seaborn** - statistical visualization

**Machine Learning Libraries (Weeks 8-13):**
- **scikit-learn** - all ML models and evaluation

**Additional Tools:**
- CSV/Excel file handling
- Basic SQL concepts (joins in pandas)
- Git/GitHub for assignment submission

**File Formats:**
- Quarto markdown (.qmd) for book chapters
- Jupyter notebooks (.ipynb) for examples, labs, homework
- Real datasets (CSV, Excel) in `/data/` directory

## Content Style

**Writing Style:**
- **Conversational and approachable** - Not dry or overly academic
- **Student-focused** - Addresses "you" directly
- **Motivational** - Builds confidence, normalizes struggle
- **Practical** - Always tied to real-world application
- **Honest** - Acknowledges difficulties, doesn't sugar-coat challenges

**Explanation Approach:**
1. **Start with WHY** - Motivate the topic before diving in
2. **Use analogies and stories** - Make abstract concepts concrete
3. **Show, don't just tell** - Working code examples over theory
4. **Progressive complexity** - Start simple, build gradually
5. **Address common questions** - Anticipate student concerns

**Examples:**
- Use **relatable business scenarios** (customer data, marketing analytics, retail transactions)
- Work with **messy, real-world datasets** (not clean, perfect examples)
- Include **visual aids** heavily (plots, diagrams, screenshots)
- Provide **executable code** that students can run and modify

**Pedagogical Elements:**
- **Callout boxes** for tips, warnings, reflections, and examples
- **Student reflection prompts** to encourage metacognition
- **Exercises** that build on chapter concepts
- **Code comments** that explain what's happening
- **Error messages and debugging guidance**

**Depth:**
- Prioritize **intuition over mathematical rigor**
- Show code implementation before heavy theory
- Balance "just enough math" with practical application
- Focus on **interpretation and application** over derivations

## Key Topics

**Module 1: Python Fundamentals (Week 1)**
- Course intro + motivation
- Variables, data types, basic operators
- Why Python? Why not just use AI?
- Setting up environment

**Module 2: Jupyter & Data Structures (Week 2)**
- Jupyter notebooks and reproducible workflows
- Lists, dictionaries, tuples
- Pandas introduction
- Importing CSV data

**Module 3: Data Wrangling (Week 3)**
- DataFrame manipulation
- Filtering and subsetting
- Aggregating data
- GroupBy operations

**Module 4: Advanced Data Manipulation (Week 4)**
- Working with dates and times
- String operations
- Relational data and joins (SQL-style in pandas)
- Merging DataFrames

**Module 5: Data Visualization (Week 5)**
- Matplotlib basics
- Seaborn for statistical plots
- Exploratory data analysis with visuals
- Best practices for effective visualization

**Module 6: Writing Efficient Code (Week 6)**
- Control flow (if/else, loops)
- Functions and modularity
- List comprehensions
- Code efficiency and readability

**Week 7: Midterm Project**
- Application of Modules 1-6
- Work with messy, real datasets
- Open-ended analysis problem

**Module 7: Machine Learning Intro (Week 8)**
- What is ML and when to use it?
- Train/test split
- Features and labels
- Model building process

**Module 8: Regression (Week 9)**
- Correlation analysis
- Linear regression with scikit-learn
- Model evaluation (R², RMSE)
- Interpretation

**Module 9: Classification (Week 10)**
- Logistic regression
- Classification metrics (accuracy, precision, recall, F1)
- Confusion matrices
- When to use classification vs regression

**Module 10: Tree-Based Models (Week 11)**
- Decision trees
- Random forests
- Feature importance
- Model interpretation

**Module 11: Model Optimization (Week 12)**
- Feature engineering
- Cross-validation
- Hyperparameter tuning (GridSearchCV)
- Model selection

**Module 12: Advanced Topics (Week 13)**
- Unsupervised learning (clustering, PCA)
- Deep learning overview
- Introduction to LLMs and GenAI concepts

**Week 14: Final Project**
- Comprehensive data science project
- Full pipeline from data cleaning to modeling

## Assessment Approach

**Grading Components:**
- **Labs** - Weekly hands-on activities (Thursdays)
- **Homework** - Applied assignments (with answer keys for instructor)
- **Midterm Project** - Comprehensive application of Modules 1-6
- **Final Project** - End-to-end data science project
- **Quizzes** - Knowledge checks (materials in `/planning/quizzes/`)

**Student Support:**
- Canvas discussion boards for peer collaboration
- Office hours
- Answer keys provided for labs and homework (instructor use)
- Multiple formats (notebook, HTML, PDF) for accessibility

**GenAI Policy:**
- **Encouraged** to use ChatGPT, Claude, Copilot as learning aids
- **Required** to understand code, not just copy it
- Emphasis on using AI to learn, not to avoid learning
- Students asked to reflect on AI tool use and limitations

**Project Structure:**
- Templates provided for major assignments
- Rubrics included in `/planning/projects/`
- Real-world datasets required
- Open-ended problems that require creative problem-solving

## Content Format

**Textbook:** Quarto book with modules 1-6 + appendices
**Slides:** Weekly presentations using Quarto + Reveal.js
**Examples:** Numbered sequence of Jupyter notebooks (01-17)
**Labs:** Weekly hands-on activities with answer keys
**Homework:** Individual assignments with solutions in multiple formats
**Datasets:** Real-world data in `/data/` directory (retail, airlines, housing, etc.)

## Course Materials Repository

All materials maintained in Git repository with structure:
- `/book/` - Textbook chapters
- `/slides/` - Weekly presentations
- `/example-notebooks/` - Companion code examples
- `/labs/` - Hands-on activities
- `/homework/` - Assignments
- `/data/` - Datasets
- `/planning/` - Instructor resources (Canvas docs, rubrics, quizzes)
