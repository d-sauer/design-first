# DesignFirst

> AI-assisted software design that amplifies human thinking, not replaces it.

---

🚧 **Development in progress** — switch to [`dev`](../../tree/dev) branch for latest updates.

---

## What is DesignFirst?

A methodology for using AI to elevate architectural thinking and deliver reliable, long-lived software.

Because code was never the hard part — understanding the problem is.

## Core Philosophy

- **Design before code** — structure first, generation second
- **Simple, not easy** — deliberate design over quick shortcuts
- **Amplify thinking** — AI challenges and questions, not just obeys
- **Stay in control** — humans own synthesis, critical thinking, and judgment

## Why?

In today's world of instant code generation, the pressure shifts upstream. DesignFirst applies AI where it matters: helping you understand, untangle, and structure problems — so the code that follows is reliable, predictable, and built to last.

---

## Quick Start

### Prerequisites

- [Claude CLI](https://docs.anthropic.com/en/docs/claude-cli) installed
- Clone this repository

### Commands

### Workflow

1. **Create Work Item**
```
   /work-item
```
   Creates the folder structure for your work item.

2. **Research**
   - Fill in predefined templates in the `research/` folder
   - Add any additional research documents

3. **Design**
   - **Product Requirements**
```
     /product-requirement-document
```

Analyzes your research and guides you through detailed questions. Outputs a Product Requirement Document.



   - **Architecture**
```
     /architecture-design
```
     
Analyzes research and product requirements, then guides you through architecture decisions. On completion, offers next design stages:

  - `/system-landscape`
  - `/system-context`
  - `/system-container`
  - `/system-container-component`
  - `/system-deployment`


Each command guides you through a structured workflow, from problem definition to architecture to decision capture.

---

## Purpose

This repository provides a systematic approach to software development by:

- Creating organized work items with consistent structure
- Guiding teams through research, product definition, architecture, and engineering phases
- Capturing architectural decisions and technology choices
- Generating C4 model architecture diagrams
- Maintaining organization-wide standards and best practices
- Integrating visual collaboration through Miro boards

## Folder Structure

```
.
├── work/                    # Active work items and projects
│   └── <work-item-name>/    # Individual work item
│       ├── research/        # Research findings and analysis
│       ├── product/         # Product requirements and specifications
│       └── architecture/    # Architecture documentation and diagrams
├── standards/               # Organization-wide standards
│   ├── adr/                # Architecture Decision Records
│   ├── rfc/                # Request for Comments
│   └── technology-repository/ # Approved/Disaproved technologies
└── .claude/
    └── skills/             # AI-powered guided workflows
```

---

## ToDo

- [ ] Apply DDD as SKILL
- [ ] Domain modeling and bounded contexts, before component diagram
- [ ] Create NFR skills to outline better non functional requirements, at he beginning of architecture design
- [ ] Put Mermaide diagrams in separate standalone files
- [ ] Add setup to run locall C4 Structurizr
- [ ] Generate plan of execution / tasks

---

## License

MIT