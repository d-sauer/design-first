# Architecture Folder

A structured workspace for architects, product managers, and engineers to collaboratively define, plan, design, and document software work items using guided AI-powered skills.

## Purpose

This repository provides a systematic approach to software development by:

- Creating organized work items with consistent structure
- Guiding teams through research, product definition, architecture, and engineering phases
- Capturing architectural decisions and technology choices
- Generating C4 model architecture diagrams
- Maintaining organization-wide standards and best practices
- Integrating visual collaboration through Miro boards

## Folder Structure

```
.
├── work/                    # Active work items and projects
│   └── <work-item-name>/    # Individual work item
│       ├── research/        # Research findings and analysis
│       ├── product/         # Product requirements and specifications
│       └── architecture/    # Architecture documentation and diagrams
├── standards/               # Organization-wide standards
│   ├── adr/                # Architecture Decision Records
│   ├── rfc/                # Request for Comments
│   └── technology-repository/ # Approved technologies
└── .claude/
    └── skills/             # AI-powered guided workflows
```

## Available Skills

Skills are AI-powered workflows that guide you through specific processes. Invoke them using `/skill-name`.

### Work Item Management

**`/work-item`** - Create new work item

- Sets up folder structure for research, product, architecture
- Establishes organized workspace for the entire lifecycle

### Product Definition

**`/product-requirement-document`** - Define product requirements

- Captures WHAT and WHY (not HOW)
- Defines capabilities, user flows, and success metrics
- Uses RPG (Repository Planning Graph) methodology
- Outputs: Product Requirements Document (PRD)

**`/critical-thinking`** - Apply critical analysis

- Questions assumptions and explores alternatives
- Identifies blind spots and latent topics
- Broadens understanding through structured inquiry

### Architecture & Design

**`/system-context`** - Document system context (C4 Level 1)

- Maps actors, external systems, and interactions
- Defines system boundaries
- Creates big-picture view for all stakeholders

**`/system-container`** - Document containers (C4 Level 2)

- Decomposes system into applications, services, data stores
- Documents technology choices and communication patterns
- Shows runtime architecture

**`/system-container-component`** - Document components (C4 Level 3)

- Breaks down containers into functional components
- Documents interfaces and responsibilities
- Shows detailed structural design

**`/system-deployment`** - Document deployment (C4 Deployment)

- Maps containers to infrastructure
- Documents environments (dev/staging/prod)
- Captures scaling and redundancy patterns

**`/system-landscape`** - Document enterprise landscape (C4 Level 0)

- Captures broader organizational context
- Shows how systems relate across the enterprise

**`/architecture-design`** - General architecture design

- Architecture design and mapping of solutions
- Flexible approach for various architecture tasks

### Decision & Standards Management

**`/adr`** - Create Architecture Decision Record

- Documents significant architectural decisions
- Captures context, options, and rationale
- Maintains decision history

**`/technology-registration`** - Register technology

- Adds technology to approved repository
- Documents purpose, constraints, and governance
- Maintains technology standards

## Workflow

### 1. Start a New Work Item

```
/work-item
```

Answer the prompts to create a structured work item folder.

### 2. Define Product Requirements

```
/product-requirement-document
```

Work through guided questions to define:

- What problem you're solving and for whom
- Key capabilities and user flows
- Success metrics and constraints
- Must-have vs nice-to-have features

### 3. Design Architecture

Document your system using the C4 model:

```
/system-context          # Start with big picture
/system-container        # Define major components
/system-container-component  # Detail internal structure
/system-deployment       # Map to infrastructure
```

### 4. Capture Decisions

As you make significant architectural choices:

```
/adr                     # Document important decisions
/technology-registration # Register new technologies
```

### 5. Apply Critical Thinking

At any stage, validate your approach:

```
/critical-thinking       # Question assumptions, explore alternatives
```

## Standards

The `standards/` folder contains organization-wide conventions:

- **ADR**: Template and examples for architecture decisions
- **RFC**: Process for proposing changes
- **Technology Repository**: Approved technologies and guidelines

## Best Practices

1. **Start with WHAT and WHY, not HOW**
   - Focus on capabilities and outcomes first
   - Defer technical decisions until architecture phase

2. **Follow the natural progression**
   - Research → Product → Architecture → Engineering
   - Each phase builds on the previous

3. **Document decisions as you go**
   - Use ADRs for significant choices
   - Capture context while it's fresh

4. **Think critically**
   - Challenge assumptions early
   - Consider alternatives before committing

5. **Keep it simple**
   - Use the minimum documentation needed
   - Focus on clarity over completeness

## Getting Started

1. Clone this repository
2. Start a new work item: `/work-item`
3. Follow the guided workflow
4. Reference existing work items in `work/` for examples

## ToDo

- [ ] Apply DDD principles as SKILL
- [ ] Domain modeling and bounded contexts, before component diagram
- [ ] Create NFR skills to outline better non functional requirements, at he beginning of architecture design
- [ ] Put Mermaide diagrams in separate standalone files
- [ ] Add setup to run locall C4 Structurizr
- [ ] Generate plan of execution / tasks

## Questions?

The skills are designed to guide you interactively. Just invoke a skill and follow the prompts. Each skill will ask clarifying questions and help you create the appropriate documentation.
