# C4 Model Reference

## System Context Diagram Deep Dive

### Purpose
The system context diagram is the starting point for documenting software architecture. It answers: "What is the system and who/what interacts with it?"

### Scope
- Single software system
- Its immediate environment (users and external systems)

### Primary Elements

**Software System in Scope**: The system being documented, shown as the central element.

**Supporting Elements**:
- **People**: Users, actors, roles, personas who interact directly with the system
- **External Software Systems**: Dependencies outside your system boundary that you don't own

### Abstraction Level
- NO technical details (protocols, databases, APIs)
- NO internal structure
- Focus on WHAT, not HOW

### Common Mistakes to Avoid
1. Including too much technical detail
2. Showing internal components
3. Missing key user types
4. Forgetting external dependencies
5. Vague or missing interaction descriptions

## Relationship to Other C4 Diagrams

```
System Landscape (Level 0) - Multiple systems in an enterprise
        ↓
System Context (Level 1) - Single system + environment  ← THIS SKILL
        ↓
Container (Level 2) - Internal high-level building blocks
        ↓
Component (Level 3) - Components within containers
        ↓
Code (Level 4) - Classes, interfaces (usually auto-generated)
```

## When to Use System Landscape vs System Context

| Aspect | System Landscape | System Context |
|--------|------------------|----------------|
| Scope | Enterprise/organization | Single system |
| Focus | How systems relate | How one system fits in environment |
| Audience | Portfolio managers, architects | Development team, stakeholders |
| Use when | Managing multiple systems | Documenting one system |

## Mermaid C4 Syntax Quick Reference

```mermaid
C4Context
    title System Context Diagram

    %% People
    Person(alias, "Label", "Description")
    Person_Ext(alias, "Label", "Description")  %% External person

    %% Systems
    System(alias, "Label", "Description")
    System_Ext(alias, "Label", "Description")  %% External system

    %% Boundaries
    Enterprise_Boundary(alias, "Label") {
        %% elements inside
    }

    %% Relationships
    Rel(from, to, "Label")
    Rel(from, to, "Label", "Technology")
    BiRel(a, b, "Label")  %% Bidirectional
```
