---
description: Ask a question about the repository and get an evidence-based answer
---

# Deep Wiki: Ask

Answer a specific question about the repository with evidence-based citations.

## Process

### Step 1: Source Repository Resolution

1. Run `git remote get-url origin` to detect remote URL
2. Ask the user if not already provided: _"Source repo URL? (or 'local' for local-only citations)"_
3. Determine branch: `git rev-parse --abbrev-ref HEAD`
4. Store citation format:
   - **Remote**: `[file:line](REPO_URL/blob/BRANCH/file#Lline)`
   - **Local**: `(file:line)`

### Step 2: Research Answer

1. **Understand the question** — clarify if ambiguous
2. **Identify relevant files** — scan for likely sources
3. **Read the code** — trace actual implementations
4. **Formulate answer** — ground every claim in evidence
5. **Cite sources** — link to specific files and lines

### Step 3: Response Format

```markdown
## Question: [user's question]

### Answer

[Clear, concise answer in 1–3 paragraphs]

### Evidence

| Source | Relevance |
|--------|-----------|
| [src/file.ts:42](REPO_URL/blob/BRANCH/src/file.ts#L42) | Shows implementation of X |
| [docs/config.md:15](REPO_URL/blob/BRANCH/docs/config.md#L15) | Documents configuration |

### Diagram (if helpful)

```mermaid
graph LR
  A --> B
```
<!-- Sources: src/file.ts:42 -->

### Related Documentation

- [Component Guide](../03-components/component.md)
- [Architecture Overview](../02-architecture/overview.md)
```

### Requirements

- **No hand-waving** — every claim must have a source citation
- **Trace actual code** — don't guess from file names
- **Be concise** — answer the question directly
- **Use diagrams** when they clarify the answer
- **Link to related docs** if they exist

### Example

```markdown
## Question: What database migrations exist?

### Answer

The project uses TypeORM migrations located in `src/migrations/`. There are 12 migrations covering user tables, authentication, and data model evolution. The latest migration (20240101000000-AddUserProfile.ts) adds a user_profile table.

### Evidence

| Source | Relevance |
|--------|-----------|
| [src/migrations/](REPO_URL/tree/BRANCH/src/migrations/) | Migration files directory |
| [src/migrations/20240101000000-AddUserProfile.ts:15](REPO_URL/blob/BRANCH/src/migrations/20240101000000-AddUserProfile.ts#L15) | Latest migration implementation |
| [package.json:42](REPO_URL/blob/BRANCH/package.json#L42) | TypeORM dependency |

### Related Documentation

- [Database Schema](../05-data/schema.md)
- [Setup Guide](../02-getting-started/setup.md#database-configuration)
```

$ARGUMENTS
