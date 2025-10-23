# Plugins

This marketplace contains a collection of Claude Code plugins designed to streamline work documentation and project management for 84.51 and University of Cincinnati.

## Available Plugins

### note-taker

**Description:** Automates note-taking by analyzing project work and creating structured notes using templates.

**Architecture Pattern:** Full Plugin with Skills (Agent + Commands + Skills)

**Components:**

**Agent:**
- `documentation-assistant` - Expert in analyzing work sessions and creating structured documentation from conversation history and git data

**Commands:**
- `/note-taker:document-work` - Guides you through documenting your work session by analyzing git commits and Claude Code conversation history, then creating a structured note based on templates

**Skills:**
- `organization-config/` - Configuration for organizations (84.51, UC) including dynamic template and save location discovery
- `content-generation/` - Strategies for analyzing work and generating intelligent content proposals for each template field

**Features:**
- Analyzes Claude Code conversation context as primary information source
- Supplements with git commits and file changes
- Dynamic template discovery (no hardcoded lists)
- Dynamic save location discovery
- Supports multiple organizations (84.51 and UC)
- Interactive workflow with intelligent content proposals
- Progressive disclosure: loads skills only when needed

**Token Efficiency:**
- Command: ~60 tokens (workflow orchestration)
- Agent: ~150 tokens (core expertise)
- Skills: ~250 tokens total (loaded only when needed)
- Total at rest: ~50 tokens (metadata only)

**Usage:**
1. After completing work, run `/note-taker:document-work`
2. The documentation-assistant agent will:
   - Analyze your conversation and git history
   - Ask which organization (84.51 or UC)
   - Dynamically discover and present available templates
   - Let you select template and save location
   - Generate intelligent content proposals for each field
   - Make it easy to accept proposals (just press Enter)
   - Save the completed note automatically

**Template Organization:**
- **84.51:** Templates prefixed with `8451-` or legacy names in `/Users/b294776/Desktop/Notes/templates/`
- **UC:** Templates prefixed with `uc-` in `/Users/b294776/Desktop/Notes/templates/`
- Templates are discovered dynamically using Glob patterns

---

### marketplace-dev

**Description:** Tools and expertise for building plugins that align with marketplace architecture.

**Agent:**
- `plugin-architect` - Expert in designing and building Claude Code plugins following marketplace architecture principles

**Commands:**
- `/marketplace-dev:create-plugin` - Interactive workflow to scaffold a new plugin with proper structure, components, and documentation
- `/marketplace-dev:validate-plugin` - Comprehensive validation of plugin architecture and compliance with marketplace principles

**Skills:**
- `architecture-principles/` - Deep knowledge of single responsibility, composability, context efficiency, and design patterns
- `plugin-templates/` - Ready-to-use templates for agents and commands with detailed guidelines

**Features:**
- Guides plugin design following single responsibility principle
- Ensures optimal component count (3-4 average)
- Validates composability and context efficiency
- Provides comprehensive templates and examples
- Generates quality validation reports
- Teaches marketplace best practices

**Usage:**

**Creating a New Plugin:**
1. Run `/marketplace-dev:create-plugin`
2. Answer questions about the problem and scope
3. Review recommended design pattern
4. Provide plugin details (name, description, components)
5. The command will scaffold the complete plugin structure
6. Documentation will be automatically updated

**Validating an Existing Plugin:**
1. Run `/marketplace-dev:validate-plugin`
2. Specify which plugin to validate
3. Review the comprehensive validation report
4. Implement recommended improvements
5. Re-validate to ensure compliance

**Consulting the Plugin Architect:**
- Ask questions about plugin design
- Get recommendations on architecture
- Review design patterns
- Learn best practices

**Architecture Principles:**
- **Single Responsibility:** Each plugin does one thing well (3-4 components average)
- **Composability:** Plugins work independently and can be combined
- **Context Efficiency:** Minimal token usage through progressive disclosure
- **Quality Standards:** Clear documentation and proper structure

**Design Patterns Supported:**
1. Single-Purpose Command (simple tools)
2. Agent + Commands (domain expertise with automation)
3. Full Plugin with Skills (complex domains with knowledge)
4. Workflow Orchestration (multi-step processes)

---

### course-builder

**Description:** Create educational content for data science, ML, AI, and MLOps courses.

**Architecture Pattern:** Full Plugin with Skills (Agent + Commands + Skills)

**Components:**

**Agent:**
- `course-architect` - Expert in creating pedagogically sound educational content tailored to different student levels and course objectives

**Commands:**
- `/course-builder:write-chapter` - Write a textbook chapter for a specific course
- `/course-builder:create-quiz` - Generate a quiz to assess student understanding
- `/course-builder:create-companion-nb` - Create a Jupyter notebook that accompanies a chapter
- `/course-builder:create-lab-nb` - Generate a hands-on lab assignment notebook
- `/course-builder:create-slides` - Create presentation slides for a lecture

**Skills:**
- `pedagogy/` - General data science teaching principles (hands-on learning, visual learning, incremental complexity)
- `content-templates/` - Structural templates for chapters, quizzes, notebooks, and slides
- `courses/intro-to-data-mining/` - Course-specific profile for Intro to Data Mining (undergrad)
- `courses/statistical-computing/` - Course-specific profile for Statistical Computing (grad)
- `courses/ml-in-business/` - Course-specific profile for ML in Business (grad)

**Features:**
- Course-aware content creation (adapts to student level and prerequisites)
- Progressive loading of course-specific context
- Balances theory with practical application
- Uses appropriate tools and libraries for each course
- Creates executable code examples and notebooks
- Supports multiple courses with different audiences and philosophies

**Token Efficiency:**
- Commands: ~80 tokens each (workflow orchestration)
- Agent: ~200 tokens (pedagogical expertise)
- Pedagogy skill: ~400 tokens (general teaching principles)
- Templates skill: ~600 tokens (content structures)
- Course profiles: ~200 tokens each (loaded only for selected course)
- Total at rest: ~60 tokens (metadata only)
- In use: 280-880 tokens depending on command and course

**Usage:**
1. Run a command (e.g., `/course-builder:write-chapter`)
2. The course-architect agent will:
   - Ask which course (Intro to Data Mining, Statistical Computing, or ML in Business)
   - Load the appropriate course profile
   - Ask for topic and parameters
   - Generate content appropriate for that course's:
     - Student level (undergrad vs grad)
     - Technical stack (pandas/sklearn vs numpy/scipy vs MLflow/K8s)
     - Learning philosophy (hands-on vs theory-driven vs applied)
     - Content style and depth
3. Review and use the generated content

**Course Profiles:**
Each course has a profile skill that defines:
- Audience and prerequisites
- Learning philosophy and teaching approach
- Technical stack (libraries, tools, environment)
- Content style (depth, examples, explanation style)
- Key topics covered
- Assessment approach

**Extensibility:**
Add new courses by creating a new course profile in `skills/courses/{course-name}/course-profile.md`

---

## Adding New Plugins

To add a new plugin to this marketplace:

1. Create a new directory under `plugins/`:
   ```
   plugins/your-plugin-name/
   ├── commands/        # Slash commands
   ├── agents/          # (optional) AI agents
   └── skills/          # (optional) Agent skills
   ```

2. Add your plugin to `.claude-plugin/marketplace.json`:
   ```json
   {
     "name": "your-plugin-name",
     "source": "./plugins/your-plugin-name",
     "description": "Brief description of what your plugin does"
   }
   ```

3. Create command files in the `commands/` directory as markdown files

4. Update this documentation to include information about your new plugin
