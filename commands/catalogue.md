---
description: Generate a hierarchical JSON catalogue (table of contents) for the repository's wiki structure
---

# Deep Wiki: Catalogue Generation

Generate a hierarchical JSON structure representing the documentation table of contents for this repository. This catalogue will be used to generate wiki pages.

## Process

### Step 1: Source Repository Resolution

1. Run `git remote get-url origin` to detect remote URL
2. Ask the user if not already provided: _"Source repo URL? (or 'local' for local-only citations)"_
3. Determine branch: `git rev-parse --abbrev-ref HEAD`
4. Store citation format:
   - **Remote**: `[file:line](REPO_URL/blob/BRANCH/file#Lline)`
   - **Local**: `(file:line)`

### Step 2: Repository Analysis

Scan the repository to identify:
- Entry points and main components
- Architecture layers and boundaries
- Key modules and their responsibilities
- Integration points and external dependencies
- Configuration and deployment patterns

### Step 3: Generate Hierarchical Catalogue

Produce a JSON structure with these properties:

```json
{
  "title": "Project Name Documentation",
  "description": "Comprehensive technical documentation for Project Name",
  "sections": [
    {
      "title": "Getting Started",
      "description": "Overview, setup, and basic usage",
      "children": [
        {
          "title": "Overview",
          "description": "Project purpose and architecture",
          "prompt": "Generate overview page covering project purpose, architecture diagram, and key components. Sources: src/main.ts:1, README.md:1",
          "file": "index.md"
        },
        {
          "title": "Setup",
          "description": "Installation and configuration",
          "prompt": "Generate setup guide with prerequisites, install commands, and configuration. Sources: package.json:1, .env.example:1",
          "file": "01-getting-started/setup.md"
        }
      ]
    },
    {
      "title": "Deep Dive",
      "description": "Detailed technical documentation",
      "children": [
        {
          "title": "Architecture",
          "description": "System design and components",
          "prompt": "Generate architecture page with component diagram, data flow, and module relationships. Sources: src/app.ts:1, src/server.ts:1",
          "file": "02-architecture/overview.md"
        },
        {
          "title": "Data Layer",
          "description": "Database schema and models",
          "prompt": "Generate data layer documentation with ER diagram and model definitions. Sources: src/models/*.ts:1",
          "file": "03-data/models.md"
        }
      ]
    }
  ]
}
```

### Rules

- Max 4 levels of nesting
- ≤8 children per section
- Every `prompt` field must include source file citations
- Derive titles from actual code structure, not templates
- For small repos (≤10 files), keep it simple with just "Getting Started"

### Output

Return the JSON catalogue as a code block for use in wiki generation.

$ARGUMENTS
