# Architecture - Draft

Use this document to draft some of your ideas about the Tech Registry Portal system architecture.

## Part 1: System Landscape (Optional)

**Use this section if you need to document how this system fits into a broader enterprise landscape.**

### Landscape Overview
- How would you name your enterprise landscape?
- What are the main systems in your enterprise?
- How do those systems interact and what are the interactions about?

## Part 2: System Context

**Document how your system fits within its environment - who uses it and what it connects to.**

### System Identity
- **System Name:** Tech Registry Portal
- **Primary Purpose:** [1-2 sentences - what does this system do?]
- **Owner/Maintainer:** [Who owns/maintains this system?]

### People/Actors
**Identify each type of user:**

#### Actor: [Role Name - e.g., Developer, Architect, Tech Lead]
- **What do they use the system for?**
- **How frequently do they interact?**

#### Actor: [Role Name]
- **What do they use the system for?**
- **How frequently do they interact?**

[Add more actors as needed]

### External Systems
**Identify systems this portal needs to integrate with:**

#### External System: [Name - e.g., Identity Provider, Source Control, etc.]
- **Internal or External?** [Same org or third-party?]
- **What data/functionality does the portal GET FROM it?**
- **What data/functionality does the portal SEND TO it?**

#### External System: [Name]
- **Internal or External?**
- **What data/functionality does the portal GET FROM it?**
- **What data/functionality does the portal SEND TO it?**

[Add more external systems as needed]

### Interactions
**Map the key relationships:**

| Source | Target | Interaction Description | Protocol/Method |
|--------|--------|------------------------|-----------------|
| [Actor/System] | Tech Registry Portal | [e.g., "Browses technology catalog"] | [e.g., HTTPS] |
| Tech Registry Portal | [External System] | [e.g., "Authenticates users"] | [e.g., OAuth 2.0] |

[Add more rows as needed]

## Part 3: System Containers

**Break down the system into its major technical building blocks.**

### Container Identification

#### Container: [Name - e.g., "Web Application", "API Service", "Database"]
- **Type:** [Application, Service, Database, File Store, Message Queue, etc.]
- **Technology:** [e.g., "React SPA", "Node.js Express", "PostgreSQL 15"]
- **Responsibility:** [What does this container do? 1-2 sentences]

#### Container: [Name]
- **Type:**
- **Technology:**
- **Responsibility:**

[Add more containers as needed]

### Container Types Checklist
Consider which of these you need:
- [ ] Web applications (server-rendered)
- [ ] Single-page applications (client-side)
- [ ] Mobile applications
- [ ] Backend services / APIs
- [ ] Databases (relational, document, graph)
- [ ] Caches
- [ ] Message queues / event buses
- [ ] File storage
- [ ] Scheduled jobs / workers

### Container Relationships
**How do containers communicate?**

| Source Container | Target Container | Description | Protocol/Technology |
|------------------|------------------|-------------|---------------------|
| [Container 1] | [Container 2] | [e.g., "Reads/writes user data"] | [e.g., "HTTPS/REST"] |

[Add more rows as needed]

### External Connections
**Which containers connect to external elements?**

- **People Entry Points:** [Which containers do users directly access?]
- **External System Integration Points:** [Which containers connect to external systems?]

## Part 4: Technology Decisions

### Key Technology Choices
- **Frontend:** [Technology and rationale]
- **Backend:** [Technology and rationale]
- **Database:** [Technology and rationale]
- **Authentication:** [Technology and rationale]
- **Hosting/Deployment:** [Technology and rationale]

### Trade-offs & Alternatives Considered
[Document key architectural decisions and why alternatives were not chosen]

## Notes & Open Questions
[Capture any additional architectural thoughts, concerns, or questions]
