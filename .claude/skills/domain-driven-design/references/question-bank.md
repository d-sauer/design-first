# Domain Analysis Question Bank

## Initial Domain Understanding

### Business Problem
- What business problem are you trying to solve?
- Who are the main users/actors in this system?
- What are the key business goals?
- What are the main workflows or processes?
- What business rules must be enforced?

### Domain Scope
- What is included in this domain?
- What is explicitly outside this domain?
- What existing systems does this interact with?
- Are there sub-domains within this larger domain?

## Identifying Entities

### Identity Questions
- What objects need to be tracked over time?
- What objects need unique identifiers?
- What objects change state throughout their lifecycle?
- What objects do users reference by ID?
- What objects have a lifecycle (created, modified, completed, archived)?

### Entity-Specific
- What states can this entity be in?
- Who can modify this entity?
- What triggers state changes?
- What invariants must always be true?
- When is this entity created/destroyed?

## Identifying Value Objects

### Attribute Questions
- What data is purely descriptive with no identity?
- What objects are defined entirely by their attributes?
- What data is immutable once created?
- What data can be compared for equality by value?
- What measurements, quantities, or descriptors exist?

### Value Object-Specific
- Can two instances with same values be swapped?
- Does this need to be validated as a unit?
- Should this be shared across multiple entities?

## Identifying Aggregates

### Consistency Questions
- What objects must be consistent with each other?
- What is the minimal unit of consistency?
- What objects are always loaded/saved together?
- What is the transaction boundary?
- What is the root entity that controls access?

### Aggregate-Specific
- What entities/value objects belong to this cluster?
- What consistency rules span multiple objects?
- What should outsiders never directly access?
- What is loaded as a complete unit?

## Domain Events

### Event Questions
- What significant things happen in this domain?
- What changes trigger notifications?
- What do other parts of the system need to know about?
- What actions complete a business process?
- What are the key milestones in workflows?

### Event-Specific
- When does this event occur?
- What data is relevant at that moment?
- Who needs to know about this event?
- What happens as a result of this event?

## Bounded Context Identification

### Context Questions
- Are there different teams working on different parts?
- Does the same term mean different things in different areas?
- Are there natural seams in the domain?
- What areas have different rates of change?
- What areas have different scalability needs?

### Context Boundaries
- What crosses context boundaries?
- How do contexts communicate?
- What is shared vs. what is context-specific?
- Where are translation layers needed?

## Ubiquitous Language

### Language Questions
- What terms do domain experts use?
- Are there multiple terms for the same concept?
- Are there ambiguous terms that need clarification?
- What terms need precise definitions?
- What analogies or metaphors do experts use?

### Validation Questions
- Would a domain expert understand your model?
- Does the code match how experts describe it?
- Are you using technical terms where domain terms exist?
- Are there confusing or misleading names?

## Critical Thinking Challenges

### Complexity Challenges
- Is this entity doing too much? Should it be split?
- Are these really separate entities or just states?
- Is this aggregate too large? Should it be split?
- Are you modeling data or modeling behavior?

### Boundary Challenges
- Should this be in a different bounded context?
- Is this domain concern or application concern?
- Is this business logic or technical infrastructure?
- Are you mixing different levels of abstraction?

### Pattern Challenges
- Why is this an entity instead of a value object?
- Does this aggregate really need to be this large?
- Are these events at the right granularity?
- Is this the right consistency boundary?

### Naming Challenges
- Is this name meaningful to domain experts?
- Does this name reveal intent?
- Is this term overloaded with multiple meanings?
- Can this be named more precisely?
