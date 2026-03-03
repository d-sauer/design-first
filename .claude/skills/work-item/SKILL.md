---
name: work-item
description: Create folder structure for a new work item. Work item will contain research, product, architecture and engineerng details.
---

# Product Requirements Document Creation Skill

Create folder with appropriate structure work new work item, containing folders for research, product details, architecture documents and engineering details.

## When to Use

Starting a new work item
Planning a major feature or refactor
Documenting existing product requirements or architecture.

## Workflow

1. What are you doing, what it is about, what are you solving?
   Give me a 1-2 sentence pitch describing what's the work about, what are you solving?

## Output

- Create work item folder
   - Based on the given answer propose user 3 to 5 short and descriptive name in kebab-case format.
   - Based on user selection create folder with that name in `/work` folder.
   - Create folder and file structure according to `./template/*`
- Prefill templates
   - In the new work item folder, in `research` folder, there are draft template
   - Update `product-requirement-draft.md` by creating simple set of questions based on
      - `./../product-requirement-document/SKILL.md`
   - Update `architecture-draft.md` by creating simple set of questions based on
      - `./../system-context/SKILL.md`
      - `./../system-container/SKILL.md`
      - `./../system-landscape/SKILL.md`
- Next step
   - When templates are filled in at your own peace, proceed with **product definition**, by saying `I want to define product definition`.
