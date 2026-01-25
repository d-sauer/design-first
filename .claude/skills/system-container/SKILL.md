---
name: system-container
description: Zooming into a software system to document its internal containers (applications, services, data stores). Use when decomposing a system into its runtime building blocks, documenting technology choices, showing how containers communicate, or creating Level 2 C4 diagrams. Follows from system-context documentation.
---

# System Container Skill

Create C4 model container diagram and document to show the high-level technical building blocks within a software system.

## Key Concepts

**Container** (NOT Docker): A separately runnable/deployable unit that executes code or stores data:
- Server-side apps (Java/Spring, .NET, Node.js, Python/Django)
- Client-side apps (SPA with React/Angular/Vue, mobile apps)
- Desktop applications
- Mobile applications
- IoT
- Data stores (databases, file systems, S3 buckets)
- Message brokers, queues

**Container Diagram** shows:
- All containers within the system boundary
- Technology choices for each container
- Communication protocols between containers
- How external people/systems connect to containers

## Workflow

### Step 1: Confirm Work Context

- Confirm relevant work item: `/work`
- Verify system-context documentation exists at `work/{work-item}/architecture/system-context.md`
- If missing, complete system-context first using `./../system-context/SKILL.md`

### Step 2: Identify Containers

For each container, capture:
- **Name**: Descriptive name (e.g., "Web Application", "API Service", "User Database")
- **Type**: Application, Service, Database, File Store, Message Queue, etc.
- **Technology**: Runtime/framework (e.g., "Node.js Express", "PostgreSQL 15", "Redis")
- **Responsibility**: What does this container do? (1-2 sentences)

#### Container Types Checklist
- [ ] Web applications (server-rendered)
- [ ] Single-page applications (client-side)
- [ ] Mobile applications
- [ ] Backend services / APIs
- [ ] Databases (relational, document, graph)
- [ ] Caches
- [ ] Message queues / event buses
- [ ] File storage
- [ ] Scheduled jobs / workers

### Step 3: Map Container Relationships

For each relationship between containers:
- **Source** → **Target**
- **Description**: What data/commands flow (e.g., "Reads/writes user data")
- **Protocol/Technology**: How they communicate (e.g., "HTTPS/REST", "gRPC", "JDBC", "AMQP")

### Step 4: Connect External Elements

From the system-context diagram, map how:
- People connect to which containers (entry points)
- External systems connect to which containers (integration points)

## Step 5: Explore

- Analyse answers amd apply critical thinking skill `./../critical-thinking/SKILL.md` for additional context. 


### Step 6: Generate Output

Create documentation using template: `./templates/system-container.md`

Output location: `work/{work-item}/architecture/system-container.md`

## Notation Guidelines

| Element | Representation |
|---------|----------------|
| System Boundary | Dashed box enclosing all containers |
| Container | Box with name, technology, and responsibility |
| Database | Cylinder shape |
| Person | Stick figure (from context) |
| External System | Box outside system boundary |
| Relationship | Arrow with protocol and description |

## Quality Checklist

- [ ] All containers are separately deployable units
- [ ] Technology stack is specified for each container
- [ ] Responsibilities are clear and non-overlapping
- [ ] Communication protocols are documented
- [ ] Entry points from users are clear
- [ ] Integration points with external systems are clear
- [ ] No deployment details (that's for deployment diagrams)
- [ ] No internal component structure (that's Level 3)
