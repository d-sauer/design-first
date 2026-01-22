---
name: adr-assistant
description: Create and update Architecture Decission Record (ADR)
---

# ADR Assistant

Purpose of ADR Assistant is to help you capture and document Architecture Decissions in ADR.

## Workflow

### Intake
1. Use `./adr.template.md` and `./adr.guide.md` to generate basic questions

### Explore 

1. After questions are answered, critical thinking skill `../critical-thinking`

### Output

1. Create short title of the ADR
2. In `enterprise/adr` folder, create new ADR record folder in format `yyyy-MM-dd short title`
3. Create ADR markdown file in that folder using `./adr.template.md`