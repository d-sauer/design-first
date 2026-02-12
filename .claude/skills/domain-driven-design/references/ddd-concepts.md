# Domain-Driven Design Concepts

## Core Building Blocks

### Entity
Object with unique identity that persists over time. Identity remains constant even if attributes change.

**Characteristics:**
- Has unique identifier (ID)
- Mutable state
- Lifecycle through multiple states
- Identity equality (two entities with same ID are the same)

**Examples:** User, Order, Product, Customer, Account

### Value Object
Immutable object defined by its attributes, not identity. Two value objects with same attributes are interchangeable.

**Characteristics:**
- No unique identifier
- Immutable
- Equality based on attributes
- Can be shared/reused

**Examples:** Address, Money, DateRange, EmailAddress, Coordinate, Color

### Aggregate
Cluster of entities and value objects treated as a single unit. Has one entity as the aggregate root that controls access.

**Characteristics:**
- Aggregate Root entity controls all access
- Ensures consistency boundaries
- External references only to root
- Modified as a unit

**Examples:** Order (with OrderLines), ShoppingCart (with Items), Reservation (with Tickets)

### Domain Event
Record of something significant that happened in the domain. Past tense naming.

**Characteristics:**
- Immutable
- Past tense name
- Contains relevant data
- Timestamp included

**Examples:** OrderPlaced, PaymentProcessed, UserRegistered, InventoryUpdated, ShipmentDelivered

## Strategic Design

### Bounded Context
Explicit boundary within which a domain model applies. Different contexts may have different models for same concept.

**Characteristics:**
- Clear boundaries
- Consistent model within
- Own ubiquitous language
- May have different meaning for same term across contexts

**Example:** "Customer" in Sales Context vs "Customer" in Support Context

### Ubiquitous Language
Common language shared by developers and domain experts. Used in code, conversations, and documentation.

**Guidelines:**
- Use domain expert terminology
- Avoid technical jargon with domain experts
- Ensure code matches the language
- Document terms and definitions

## Hexagonal Architecture Mapping

**Domain Layer (Center):**
- Entities
- Value Objects
- Aggregates
- Domain Events
- Domain Services

**Ports (Interfaces):**
- Inbound: Use cases, commands, queries
- Outbound: Repository interfaces, external service interfaces

**Adapters (Outside):**
- Inbound: REST controllers, GraphQL resolvers, CLI, message consumers
- Outbound: Database repositories, external API clients, message publishers

## Attribute Analysis Guidelines

When identifying attributes, classify as:

1. **Identity attributes** - Unique identifiers (for entities)
2. **Descriptive attributes** - Basic properties
3. **Behavioral attributes** - State that drives behavior
4. **Relational attributes** - References to other domain objects
5. **Temporal attributes** - Time-related data
6. **Calculated attributes** - Derived from other attributes

## Common Patterns

### Attribute Grouping
Group related attributes into:
- **Core Domain Data** - Essential business attributes
- **Technical Metadata** - Audit fields, timestamps, versions
- **Reference Data** - Lookups, classifications, categories
- **Relationships** - Connections to other aggregates/contexts
