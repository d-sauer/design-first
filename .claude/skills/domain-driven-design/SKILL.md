---
name: domain-driven-design
description: Domain-Driven Design (DDD) domain identification and analysis for hexagonal architecture. Use when users want to identify domains, define bounded contexts, map entities/value objects/aggregates, establish ubiquitous language, or prepare domain models for hexagonal architecture. Triggered by requests like "identify domain for my [domain]", "analyze this business domain", "define bounded contexts", or when starting software architecture design with domain modeling.
---

# Domain-Driven Design Domain Analysis

Guide users through structured domain analysis to identify domain models suitable for hexagonal architecture.

## Process Overview

Domain analysis follows these steps:

1. Understand the business problem and scope
2. Identify initial attributes and concepts
3. Classify domain objects (entities, value objects, aggregates)
4. Establish ubiquitous language
5. Identify domain events
6. Define bounded contexts
7. Challenge and refine through critical thinking
8. Generate comprehensive domain analysis document

## Workflow

### Step 1: Understand the Business Problem

Ask the user to describe:
- The business problem being solved
- Main users/actors in the system
- Key business goals
- Primary workflows or processes
- Critical business rules

Use questions from [references/question-bank.md](references/question-bank.md) under "Initial Domain Understanding."

### Step 2: Identify Initial Attributes

Ask the user to outline the main attributes and data the domain works with. This provides raw material for further analysis.

**Prompt the user:** "What are the main attributes or data elements this domain needs to work with?"

### Step 3: Classify Domain Objects

Read [references/ddd-concepts.md](references/ddd-concepts.md) for detailed definitions.

#### Identify Entities

Ask questions from question-bank.md "Identifying Entities" section to discover objects with:
- Unique identity
- Mutable state
- Lifecycle
- Identity-based equality

**Examples:** User, Order, Product, Customer, Account

#### Identify Value Objects

Ask questions from question-bank.md "Identifying Value Objects" section to discover objects with:
- No unique identity
- Immutable
- Attribute-based equality
- Descriptive nature

**Examples:** Address, Money, DateRange, EmailAddress

#### Identify Aggregates

Ask questions from question-bank.md "Identifying Aggregates" section to discover:
- Consistency boundaries
- Clusters of related entities/value objects
- Aggregate roots that control access
- Transaction boundaries

**Examples:** Order (with OrderLines), ShoppingCart (with Items)

### Step 4: Establish Ubiquitous Language

Use questions from question-bank.md "Ubiquitous Language" section to:
- Identify domain expert terminology
- Clarify ambiguous terms
- Document precise definitions
- Ensure code will match domain language

Create a glossary of key terms with definitions that both developers and domain experts understand.

### Step 5: Identify Domain Events

Use questions from question-bank.md "Domain Events" section to discover significant occurrences.

**Characteristics:**
- Past tense naming
- Captures moment something happened
- Contains relevant data
- Immutable

**Examples:** OrderPlaced, PaymentProcessed, UserRegistered

### Step 6: Define Bounded Contexts

Use questions from question-bank.md "Bounded Context Identification" section to:
- Identify natural seams in the domain
- Recognize where terms have different meanings
- Define clear boundaries
- Determine integration patterns between contexts

Each bounded context has its own consistent model and ubiquitous language.

### Step 7: Challenge and Refine

Apply critical thinking using challenges from question-bank.md "Critical Thinking Challenges":

**Complexity Challenges:**
- Is this entity too complex? Should it split?
- Are these separate entities or just states?
- Is this aggregate too large?

**Boundary Challenges:**
- Is this in the right bounded context?
- Is this domain or application concern?
- Is this business logic or infrastructure?

**Pattern Challenges:**
- Why entity instead of value object?
- Is the aggregate at the right size?
- Are events at proper granularity?

**Naming Challenges:**
- Would domain experts understand this name?
- Does the name reveal intent?
- Is this term overloaded?

**Important:** Challenge assumptions respectfully. Ask "why" and explore alternatives to help users refine their domain model.

### Step 8: Generate Domain Analysis Document

Use [assets/domain-analysis-template.md](assets/domain-analysis-template.md) to create a comprehensive document in `architecture` folder

**Document structure:**
1. Domain Overview - Business problem, scope, stakeholders
2. Bounded Contexts - Purpose, responsibilities, ubiquitous language
3. Domain Model - Entities, value objects, aggregates with attributes
4. Domain Events - Key events with triggers and data
5. Data Model Connections - Relationships between groups and contexts
6. Hexagonal Architecture Mapping - Domain layer, ports, adapters
7. Design Decisions & Rationale - Key choices and trade-offs
8. Open Questions - Future considerations

**Attribute Documentation:**

Group attributes into categories:
- **Core Domain Data** - Essential business attributes
- **Technical Metadata** - Audit fields, timestamps, versions
- **Reference Data** - Lookups, classifications, categories
- **Relationships** - References to other aggregates/contexts

For each attribute, document:
- Name
- Description
- Type (String, Integer, Boolean, etc.)
- Format (ISO-8601, UUID, Email, etc.)
- Group

## Tips for Effective Domain Analysis

**Stay Domain-Focused:**
- Focus on business concepts, not technical implementation
- Use domain expert language, not technical jargon
- Model behavior, not just data
- Enforce business rules in the domain

**Right-Size Components:**
- Entities: Not too large, focused on single concept
- Aggregates: Small consistency boundaries
- Contexts: Natural seams with clear boundaries
- Events: Significant business moments

**Iterative Refinement:**
- Start with broad understanding
- Drill into specifics
- Challenge assumptions
- Refine based on new insights

**Hexagonal Architecture Alignment:**
- Domain layer is the core (entities, value objects, aggregates)
- Ports define interfaces (inbound use cases, outbound dependencies)
- Adapters implement infrastructure (REST, database, external APIs)
- Dependencies point inward (infrastructure depends on domain, not vice versa)

## References

Load these files as needed:
- **[references/ddd-concepts.md](references/ddd-concepts.md)** - DDD building blocks, patterns, and hexagonal architecture mapping
- **[references/question-bank.md](references/question-bank.md)** - Comprehensive questions for each analysis phase
- **[assets/domain-analysis-template.md](assets/domain-analysis-template.md)** - Output document structure
