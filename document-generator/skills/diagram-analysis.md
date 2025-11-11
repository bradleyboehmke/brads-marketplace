---
title: Diagram Analysis
description: Understanding system architecture to choose appropriate diagram types
tags: [analysis, diagrams, architecture, visualization]
---

# Diagram Analysis

## Metadata

**Purpose**: Analyze systems to determine best diagram type and content
**Version**: 1.0.0

---

## Analysis Steps

### 1. Understand the Goal

**Ask**:
- What story needs to be told?
- Who is the audience?
- What decisions will this support?
- What level of detail is needed?

### 2. Identify Architecture Type

**Common patterns**:
- **Monolithic** - Single application, internal modules
- **Microservices** - Multiple services, APIs, message queues
- **Data pipeline** - Data flow from sources to outputs
- **ML system** - Training vs inference pipelines
- **Library/Framework** - Class hierarchies, modules

### 3. Choose Diagram Type

**For system overview**: C4 Context
**For service architecture**: C4 Container or Flowchart
**For internal structure**: C4 Component or Class Diagram
**For interactions**: Sequence Diagram
**For data models**: ER Diagram
**For processes**: Flowchart
**For state changes**: State Diagram

### 4. Determine Scope

**Include**:
- Essential components for the story
- Key relationships and dependencies
- Technology choices (if relevant to audience)

**Exclude**:
- Implementation details (unless that's the focus)
- Everything not needed for this specific diagram
- Redundant information

## Discovery Commands

**System boundaries**:
```bash
# Find services/modules
ls -d */  | head -10
find . -name "docker-compose.yml" -o -name "Dockerfile"
```

**Interactions**:
```bash
# Find API definitions
find . -name "*api*.py" -o -name "*route*.py"

# Check for message queues
grep -r "kafka\|rabbitmq\|redis\|celery" pyproject.toml requirements.txt
```

**Data flow**:
```bash
# Find data sources
find . -name "*data*" -o -name "*extract*" -o -name "*load*"

# Check databases
grep -i "postgres\|mysql\|mongo\|sqlite" pyproject.toml requirements.txt
```

## Diagram Planning

**Start simple**:
1. List main components
2. Identify key relationships
3. Choose direction (TD/LR)
4. Add labels
5. Refine as needed

**Validate**:
- Does it tell the right story?
- Is it too complex?
- Is anything missing?
- Will the audience understand it?
