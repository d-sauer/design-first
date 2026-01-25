# C4 Container Reference

## What is a Container?

A container is a **runtime boundary** - something that needs to be running for the system to work. It executes code or stores data.

**NOT Docker**: The C4 term predates Docker. A C4 container may or may not run in a Docker container.

### Container Examples

| Type | Examples |
|------|----------|
| Server-side Web App | Java/Spring MVC, ASP.NET, Rails, Django, Express |
| Client-side SPA | React, Angular, Vue running in browser |
| Mobile App | iOS (Swift), Android (Kotlin), Flutter, React Native |
| Desktop App | Electron, WPF, JavaFX |
| API Service | REST API, GraphQL server, gRPC service |
| Database | PostgreSQL, MySQL, MongoDB, DynamoDB |
| Cache | Redis, Memcached |
| Message Broker | RabbitMQ, Kafka, AWS SQS |
| File Storage | Local filesystem, S3, Azure Blob |
| Serverless Function | AWS Lambda, Azure Functions |
| Background Worker | Scheduled jobs, queue processors |

### Is it One Container or Two?

**One container**: Traditional server-rendered web app (e.g., Rails app generating HTML)

**Two containers**: 
- Server that serves API + static files
- SPA running in browser (significant JavaScript)

**Rule**: If code runs in different process spaces, they're separate containers.

## Container vs External System

| Aspect | Container | External System |
|--------|-----------|-----------------|
| Ownership | You build/maintain it | Third-party owns it |
| Responsibility | Your team | External team/vendor |
| Boundary | Inside your system | Outside your system |

**Grey area**: Cloud services like S3, RDS where you don't run them but own the data/schema. Generally treat these as containers since you have responsibility for them.

## Mermaid C4Container Syntax

```mermaid
C4Container
    title Container Diagram - System Name

    %% People (from context)
    Person(alias, "Label", "Description")
    Person_Ext(alias, "Label", "Description")

    %% System boundary
    System_Boundary(alias, "System Name") {
        %% Containers inside
    }

    %% Container types
    Container(alias, "Name", "Technology", "Description")
    ContainerDb(alias, "Name", "Technology", "Description")
    ContainerQueue(alias, "Name", "Technology", "Description")
    Container_Ext(alias, "Name", "Technology", "Description")

    %% External systems (from context)
    System_Ext(alias, "Name", "Description")

    %% Relationships with protocol
    Rel(from, to, "Label", "Protocol")
    BiRel(a, b, "Label", "Protocol")
```

## Common Mistakes

1. **Showing deployment details**: Clustering, load balancers, replicas belong in deployment diagrams
2. **Including components**: Classes, modules, packages are Level 3 (Component)
3. **Missing technology**: Always specify the tech stack
4. **Vague responsibilities**: Each container should have clear, specific purpose
5. **Forgetting data stores**: Databases and caches are containers too
6. **Mixing environments**: Show logical architecture, not dev vs prod differences

## Container Diagram Checklist

- [ ] System boundary is clearly marked
- [ ] All containers have name + technology + responsibility
- [ ] Relationships show what flows (data/commands) and how (protocol)
- [ ] External actors from context diagram are included
- [ ] External systems from context diagram are included
- [ ] No internal component details shown
- [ ] No deployment/infrastructure details shown
- [ ] Diagram has title and optional key/legend

## Relationship to Other C4 Levels

```
System Context (Level 1)
    Shows: System as single box
    ↓ ZOOM IN
Container (Level 2)  ← THIS LEVEL
    Shows: Applications, services, data stores inside system
    ↓ ZOOM IN (per container)
Component (Level 3)
    Shows: Major structural building blocks inside a container
    ↓ ZOOM IN (per component)
Code (Level 4)
    Shows: Classes, interfaces, functions
```
