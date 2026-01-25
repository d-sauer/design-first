---
name: system-component
description: Zooming into a container to document its internal components (groupings of related functionality) using the C4 model. Use when decomposing a container into its structural building blocks, documenting interfaces and responsibilities, showing component interactions, or creating Level 3 C4 diagrams. Follows from system-container documentation. Create one component diagram per container that warrants detailed documentation.
---

# System Component Skill

Create C4 model component diagrams to show the internal structure of a container - the groupings of related functionality that make up its architecture.

## Key Concepts

**Component**: A grouping of related functionality encapsulated behind a well-defined interface. NOT separately deployable - all components run in the same container process space.

Examples by paradigm:
- **OOP (Java/C#)**: Collection of classes behind an interface
- **Functional (F#/Haskell)**: Module grouping related functions and types
- **JavaScript/TypeScript**: Module or package with exported interface

**Component Diagram** shows:
- All significant components within one container
- Responsibilities of each component
- Interfaces/contracts between components
- Connections to other containers and external systems

## When to Create Component Diagrams

Component diagrams are **optional** in C4. Create them when:
- Container is complex enough to warrant decomposition
- Onboarding new developers to codebase
- Planning significant refactoring
- Documenting critical/core containers

Consider **automation** for long-lived documentation (reverse-engineering from code).

## Workflow

### Step 1: Confirm Work Context

- Confirm relevant work item: `/work`
- Verify system-container documentation exists at `work/{work-item}/architecture/system-container.md`
- Select which container to decompose

### Step 2: Identify Components

For each significant component, capture:
- **Name**: Descriptive name (e.g., "Authentication Controller", "Order Service", "Payment Gateway Facade")
- **Type**: Controller, Service, Repository, Facade, Handler, Validator, etc.
- **Technology**: Implementation details (e.g., "Spring MVC Controller", "TypeScript class")
- **Responsibility**: What functionality does this component provide? (1-2 sentences)
- **Interface**: How is this component accessed? (methods, events, API)

#### Component Identification Strategies

**By Layer** (traditional):
- Controllers / Handlers (entry points)
- Services (business logic)
- Repositories / DAOs (data access)
- Facades (external system integration)

**By Feature/Domain** (DDD-style):
- User Management Component
- Order Processing Component
- Payment Component

**By Pattern**:
- Identify interfaces and their implementations
- Group classes that change together
- Look for natural boundaries in the codebase

### Step 3: Map Component Relationships

For each relationship:
- **Source** → **Target**
- **Description**: What the source uses from target (e.g., "Uses to validate orders")
- **Method**: How they interact (e.g., "Method call", "Event", "Callback")

### Step 4: Connect External Elements

Map how components connect to:
- Other containers in the system (from container diagram)
- External systems (from context diagram)
- Databases and data stores

## Step 5: Explore

- Analyse answers amd apply critical thinking skill `./../critical-thinking/SKILL.md` for additional context. 

### Step 6: Generate Output

Create documentation using template: `./templates/system-component.md`

Output location: `work/{work-item}/architecture/components/{container-name}.md`

## Notation Guidelines

| Element | Representation |
|---------|----------------|
| Container Boundary | Dashed box enclosing all components |
| Component | Box with name, type, technology, responsibility |
| Other Container | Box outside boundary (simplified) |
| External System | Box outside boundary |
| Database | Cylinder (from container level) |
| Relationship | Arrow with description |

## Quality Checklist

- [ ] Scope is a single container
- [ ] Components represent logical groupings, not individual classes
- [ ] Each component has clear, single responsibility
- [ ] Interfaces between components are documented
- [ ] Connections to other containers shown
- [ ] No deployment details shown
- [ ] Diagram useful for developers understanding the codebase
- [ ] Consider if automation would be more maintainable
