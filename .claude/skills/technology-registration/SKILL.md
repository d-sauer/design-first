---
name: technology-registration
description: Create or update technology repository. Technology Repository is a repository of all used technologies across the organisation. USE when creating new technology or updating existing.
---

# Technology Registration

Technology is the building block used to construct applications, systems, services and IT assets that support business capabilities.
Along with the underlying infrastructure that enables their delivery and consumption, including tools, frameworks, techniques and processes employed to develop, deploy and manage those technology solutions.
Excluding “libraries”, “pure hardware” or “workplace applications”.

## Workflow

### Step 1: Basic information about technology

1. What is the name of the technology?
2. What is the purpose and intention to use this technology for?
3. What is the web page for this technology

### Step 2. Obtain more information about technology

1. Read the JSON Schema `./tech-record.schema.json`
2. Generate questions and options.
   Options are based on `const` constants in json file
   Options are based on previously provide web page
3. Ask questions and suggested answers based on given const in the schema and web page

### Step 3. Create output

1. AI create new folder using kebab case (`technology-name`) in `./enterprise/technology-repository/`
2. Create `technology-name.json` file based on template `./../../../enterprise/technology-repository/.schema/technology.template.json`
3. Create `technology-name.md` markdown file containing more details about technology using template `./template/technology-x.md` and provided answers.
4. Create `technology-name.note.md` based on template `./template/technology-x.note.md`
