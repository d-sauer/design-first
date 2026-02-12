# Domain Analysis: [Domain Name]

**Date:** [Date]
**Version:** 1.0

---

## 1. Domain Overview

### Business Problem
[Description of the business problem this domain addresses]

### Domain Scope
**In Scope:**
- [What's included]

**Out of Scope:**
- [What's explicitly excluded]

### Key Stakeholders
- [List of main users/actors]

---

## 2. Bounded Contexts

### [Context Name 1]
**Purpose:** [What this context is responsible for]

**Responsibilities:**
- [Key responsibility 1]
- [Key responsibility 2]

**Ubiquitous Language:**
| Term | Definition |
|------|------------|
| [Term] | [Definition] |

---

### [Context Name 2]
**Purpose:** [What this context is responsible for]

**Responsibilities:**
- [Key responsibility 1]
- [Key responsibility 2]

**Ubiquitous Language:**
| Term | Definition |
|------|------------|
| [Term] | [Definition] |

---

## 3. Domain Model

### Entities

#### [Entity Name]
**Description:** [What this entity represents]

**Identity:** [ID attribute and type]

**Lifecycle States:** [State1] → [State2] → [State3]

**Attributes:**

| Attribute | Description | Type | Format | Group |
|-----------|-------------|------|--------|-------|
| [name] | [description] | [type] | [format] | [group] |

**Invariants:**
- [Business rule that must always be true]

---

### Value Objects

#### [Value Object Name]
**Description:** [What this value object represents]

**Attributes:**

| Attribute | Description | Type | Format | Group |
|-----------|-------------|------|--------|-------|
| [name] | [description] | [type] | [format] | [group] |

**Validation Rules:**
- [Validation rule]

---

### Aggregates

#### [Aggregate Name]
**Description:** [What this aggregate manages]

**Aggregate Root:** [Entity name]

**Contains:**
- [Entity/Value Object 1]
- [Entity/Value Object 2]

**Consistency Boundary:** [What must remain consistent]

**Attributes by Group:**

##### Core Domain Data
| Attribute | Description | Type | Format |
|-----------|-------------|------|--------|
| [name] | [description] | [type] | [format] |

##### Technical Metadata
| Attribute | Description | Type | Format |
|-----------|-------------|------|--------|
| [name] | [description] | [type] | [format] |

##### Reference Data
| Attribute | Description | Type | Format |
|-----------|-------------|------|--------|
| [name] | [description] | [type] | [format] |

##### Relationships
| Attribute | Description | Type | Format |
|-----------|-------------|------|--------|
| [name] | [description] | [type] | [format] |

---

## 4. Domain Events

| Event Name | Trigger | Data Included | Consumers |
|------------|---------|---------------|-----------|
| [EventName] | [When it occurs] | [Key data] | [Who listens] |

---

## 5. Data Model Connections

### Relationships Between Groups

```
[Aggregate 1]
    |-- has --> [Aggregate 2]
    |-- references --> [Entity 3]
    |-- contains --> [Value Object 1]

[Context 1] <--> [Context 2]
    via: [Integration mechanism]
```

### Cross-Context Relationships

| From Context | To Context | Relationship | Integration Pattern |
|--------------|------------|--------------|---------------------|
| [Context A] | [Context B] | [Type] | [How they communicate] |

---

## 6. Hexagonal Architecture Mapping

### Domain Layer (Core)
**Entities:**
- [Entity list]

**Value Objects:**
- [Value Object list]

**Aggregates:**
- [Aggregate list]

**Domain Services:**
- [Service list]

### Ports (Interfaces)

**Inbound Ports (Use Cases):**
- [Use case 1]
- [Use case 2]

**Outbound Ports (Dependencies):**
- [Repository interface 1]
- [External service interface 1]

### Adapters (Implementation)

**Inbound Adapters:**
- REST API
- GraphQL
- Message Queue Consumer
- [Other]

**Outbound Adapters:**
- Database Repository
- External API Client
- Message Publisher
- [Other]

---

## 7. Design Decisions & Rationale

### Key Decisions
1. **[Decision Topic]**
   - **Decision:** [What was decided]
   - **Rationale:** [Why this decision was made]
   - **Trade-offs:** [What was considered]

---

## 8. Open Questions & Future Considerations

- [ ] [Question or consideration 1]
- [ ] [Question or consideration 2]
