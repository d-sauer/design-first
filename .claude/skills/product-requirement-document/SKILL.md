---
name: product-requirement-document
description: Create or update Product Requirements Document (PRD) for software project. Collect requirements, define features, and outline specifications to guide development teams. Collect obstacles, limitations, boundaries and restrictions. USE WHEN asked to create or update product.
---

# Product Requirements Document Creation Skill

Create or update Product Requirements Document (PRD) for software project.
Collect requirements, define features, and outline specifications to guide development teams.
Collect obstacles, limitations, boundaries and restrictions.
Create structured, dependency-aware Product Requirement Documents using the RPG (Repository Planning Graph) methodology.

## Overview

PRDs bridge the gap between product vision and implementation.

Separate WHAT (functional capabilities) from HOW (code structure)
Define explicit dependencies between components
Enable topological task ordering for development

## When to Use

Starting a new software project
Planning a major feature or refactor
Documenting existing product requirements.

## Workflow

- AI use following workflow to ask question by question from each step.
- Analyse `research` folder for this work item, and focus on `product-requirements-draft.md`. 
- Use `product-requirements-draft.md` to suggest answers during this stage.


### Step 1: Define the problem

1. What are you building?
   Provide user a hint: Give me a 1-2 sentence pitch describing what the product, and what problem it solves.

2. Who it is for?
   Provide user a hint: Tell me about your target audience — who they are, their pain points, and when/where they'd use the product

3. How do we measure success?
   Quantifiable outcomes.

### Step 2: Capabilities and functional decomposition

Think about what the product does, not code structure, but [[#Step 1: Define the problem]]

1. Identify high-level capability domains
   e.g., "Data Management", "Authentication", "Commerce", "Finance", "Marketing"

2. What is the main user flow?
   Provide user a hint: Map out the step-by-step experience.
   For example: Open app → Login → Find topic → Vote/Comment → submit.

3. What are the must have capabilities (for first version)?
   Which are must have, and which good to have.

4. For each capability, define:

- Description (one sentence)
- Inputs (what it needs)
- Outputs (what it produces)
- Behavior (key logic)

## Step 3: Explore

1. Analyse answers and check if there is description on HOW to build the product?
   If yes
   - make summary on WHAT and WHY and validate with the user is WHAT and WHY correct, and how is different from HOW?
   - Verify with user the difference and ask explicitly to focus on WHAT and WHY?
   
2. Apply critical thinking skill `../critical-thinking`

## Output

- Generate markdown document combining all given inputs in appropriate structure.
   - Brief product description
   - Reasoning why we need this product and why we can't use existing products.
   - Create a Mermaid mindmap diagram that provides a crisp, scannable overview of the product.
      - Format: Mermaid mindmap syntax
      - Depth: Maximum 2 levels (root → modules → capabilities)
      - Focus: WHAT the product does (not WHY it exists or HOW it works)
   - What are the main capabilities of the product with their description.
   - what are the main user flows
   - Put this document markdown in `work/<project-name>/product/product-requirement.md`.
- Generate document with quesstions being asked by AI (prompts), and raw user answers in the prompt. Put other user inputs on the end of the document.
   - Put this document markdown in `work/<project-name>/product/product-requirement-raw.md`.


