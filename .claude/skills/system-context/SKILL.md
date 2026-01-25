---
name: system-context
description: Capturing the surrounding context of a software system using the C4 model approach. Use when documenting what users and external systems interact with your system, understanding system boundaries, creating architecture documentation, or when asked about system context diagrams. Helps identify actors, external dependencies, and interaction patterns.
---

# System Context Skill

Create system context diagrams and documentation to capture how a software system fits within its environment.

## Key Concepts

**System Context Diagram** shows your system as a central box surrounded by:
- **People** (actors, roles, personas) who use it
- **External Systems** it depends on or integrates with
- **Interactions** describing what data/actions flow between them

**Focus**: Big picture, not technical details. Suitable for both technical and non-technical audiences.

## Workflow

### Step 1: Confirm Work Context

- Confirm relevant work item: `/work`
- Identify the primary software system being documented

### Step 2: Identify the System

Ask and document:
- What is the name of your system?
- What is its primary purpose (1-2 sentences)?
- Who owns/maintains this system?

### Step 3: Identify People/Actors

For each type of user:
- Role name (e.g., "Customer", "Admin", "Support Agent")
- What do they use the system for?
- How frequently do they interact?

### Step 4: Identify External Systems

For each external system:
- System name
- Is it internal (same org) or external (third-party)?
- What data/functionality does your system get FROM it?
- What data/functionality does your system send TO it?

### Step 5: Map Interactions

For each relationship, capture:
- Source → Target
- Description of interaction (verb phrase, e.g., "Sends order data", "Authenticates users")
- Protocol/method if known (optional at this level)

## Step 6: Explore

- Analyse answers amd apply critical thinking skill `./../critical-thinking/SKILL.md` for additional context. 


### Step 7: Generate Output

Create documentation using template: `./templates/system-context.md`

Output location: `work/{work-item}/architecture/system-context.md`

## Notation Guidelines

| Element | Representation |
|---------|----------------|
| Your System | Box (center) with name and brief description |
| Person | Stick figure or labeled box |
| External System | Box (different style/color from your system) |
| Relationship | Arrow with verb describing the interaction |

## Quality Checklist

- [ ] System has clear name and purpose
- [ ] All user types identified
- [ ] All external dependencies captured
- [ ] Interactions describe WHAT, not HOW
- [ ] Diagram readable by non-technical stakeholders
- [ ] No internal implementation details shown
