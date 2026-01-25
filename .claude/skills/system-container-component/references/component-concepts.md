# C4 Component Reference

## What is a Component?

A **grouping of related functionality** encapsulated behind a well-defined interface.

**Key characteristics**:
- NOT separately deployable (unlike containers)
- Runs in same process space as other components in the container
- Represents a logical grouping, not physical packaging
- Should map to real abstractions in your codebase

## Component vs Class vs Package

| Abstraction | C4 Level | Example |
|-------------|----------|---------|
| Component | Level 3 | "User Service" (multiple classes) |
| Class/Interface | Level 4 (Code) | `UserService.java`, `IUserRepository` |
| Package/Module | Orthogonal | `com.example.users` (organizational) |

Components are **between** packages and individual classes - they're meaningful architectural units.

## Identifying Components

### Strategy 1: By Interface

Look for interfaces that represent boundaries:
```
IUserService          → "User Service" component
IOrderRepository      → "Order Repository" component
IPaymentGateway       → "Payment Gateway Facade" component
```

### Strategy 2: By Layer

Traditional layered architecture:
```
Controllers/Handlers  → Entry point components
Services              → Business logic components
Repositories/DAOs     → Data access components
Facades/Adapters      → Integration components
```

### Strategy 3: By Feature/Domain

Domain-driven grouping:
```
User Management       → All user-related classes
Order Processing      → All order-related classes
Payment Handling      → All payment-related classes
```

### Strategy 4: By Change Together

Classes that typically change together belong to same component.

## Common Component Types

| Type | Purpose | Examples |
|------|---------|----------|
| Controller | HTTP/API entry point | REST controller, GraphQL resolver |
| Service | Business logic | OrderService, UserService |
| Repository | Data access | UserRepository, OrderDAO |
| Facade | External system wrapper | PaymentGatewayFacade, EmailFacade |
| Handler | Event/message processing | OrderEventHandler, WebhookHandler |
| Validator | Input validation | OrderValidator, UserValidator |
| Factory | Object creation | OrderFactory, NotificationFactory |
| Mapper | Data transformation | UserMapper, OrderDTOMapper |

## What NOT to Show as Components

- Individual classes (too granular)
- DTOs/POJOs/Value Objects (data structures, not behavior)
- Utility classes (cross-cutting, not architectural)
- Configuration classes
- Test classes

## Mermaid C4Component Syntax

```mermaid
C4Component
    title Component Diagram - Container Name

    %% Container boundary
    Container_Boundary(alias, "Container Name") {
        %% Components inside
        Component(alias, "Name", "Type", "Description")
        ComponentDb(alias, "Name", "Type", "Description")
        ComponentQueue(alias, "Name", "Type", "Description")
    }

    %% External elements (from container level)
    Container(alias, "Name", "Technology", "Description")
    ContainerDb(alias, "Name", "Technology", "Description")
    System_Ext(alias, "Name", "Description")

    %% Relationships
    Rel(from, to, "Label")
    Rel(from, to, "Label", "Method/Protocol")
```

## Component Diagram Scope

**One diagram = One container**

Create separate component diagrams for each container that needs detailed documentation.

```
system-container.md           (all containers)
    ↓
components/
    ├── api-service.md        (components in API Service)
    ├── web-application.md    (components in Web App)
    └── background-worker.md  (components in Worker)
```

## When to Automate

Consider generating component diagrams from code when:
- Codebase is large (100+ classes)
- Components change frequently
- Team wants living documentation
- Consistent structure across codebase

Tools:
- Structurizr (DSL-based)
- IDE plugins (IntelliJ, VS Code)
- Static analysis tools
- Custom scripts parsing AST

## Relationship to Other C4 Levels

```
Container (Level 2)
    Shows: Container as single box
    ↓ ZOOM IN (per container)
Component (Level 3)  ← THIS LEVEL
    Shows: Logical groupings inside container
    ↓ ZOOM IN (per component)
Code (Level 4)
    Shows: Classes, interfaces, functions
    (Often UML class diagrams or auto-generated)
```

## Common Mistakes

1. **Too granular**: Showing every class as a component
2. **Too abstract**: Components too large/vague to be useful
3. **Missing interfaces**: Not showing how components interact
4. **Deployment details**: Including clustering, instances (Level 2 or deployment diagram)
5. **Cross-container**: Mixing components from multiple containers
6. **No maintenance plan**: Creating diagrams that quickly become outdated

## Decision: Do You Need Component Diagrams?

| Situation | Recommendation |
|-----------|----------------|
| Small container (<10 classes) | Skip, code is self-documenting |
| Medium container (10-50 classes) | Create if onboarding or refactoring |
| Large container (50+ classes) | Create and consider automation |
| Rapidly changing codebase | Automate or don't create |
| Stable core container | Create once, update rarely |
| Microservices (small) | Usually skip |
| Monolith | Definitely create |
