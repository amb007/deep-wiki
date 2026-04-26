---
description: Generate llms.txt and llms-full.txt for LLM-friendly project access
---

# Deep Wiki: llms.txt Generation

Generate LLM-friendly project summaries following the [llms.txt specification](https://llmstxt.org/).

## Process

### Step 1: Source Repository Resolution

1. Run `git remote get-url origin` to detect remote URL
2. Ask the user if not already provided: _"Source repo URL? (or 'local' for local-only citations)"_
3. Determine branch: `git rev-parse --abbrev-ref HEAD`
4. Store citation format:
   - **Remote**: `[file:line](REPO_URL/blob/BRANCH/file#Lline)`
   - **Local**: `(file:line)`

### Step 2: Generate llms.txt Files

Create three files:

#### 1. `./llms.txt` (Repo Root)

Standard discovery location for coding agents.

```markdown
# Project Name

> Comprehensive technical documentation for Project Name — a system that does X, Y, and Z.

## Onboarding

- [Contributor Guide](./wiki/onboarding/contributor-guide.md) — For new contributors
- [Staff Engineer Guide](./wiki/onboarding/staff-engineer-guide.md) — Architectural deep dive
- [Executive Guide](./wiki/onboarding/executive-guide.md) — Capability map and risks
- [Product Manager Guide](./wiki/onboarding/product-manager-guide.md) — User journeys and features

## Architecture

- [Overview](./wiki/02-architecture/overview.md) — System design and components
- [Data Flow](./wiki/02-architecture/data-flow.md) — How data moves through the system
- [API Design](./wiki/02-architecture/api-design.md) — Interface contracts

## Getting Started

- [Setup](./wiki/01-getting-started/setup.md) — Installation and configuration
- [Quick Start](./wiki/01-getting-started/quick-start.md) — Run the project in 5 minutes
- [Configuration](./wiki/01-getting-started/configuration.md) — Environment variables and settings

## Deep Dive

- [Core Modules](./wiki/03-core/modules.md) — Main components and their responsibilities
- [Data Layer](./wiki/05-data/models.md) — Database schema and models
- [Integration](./wiki/06-integration/overview.md) — External service connections

## Optional

- [Changelog](./CHANGELOG.md) — Version history and changes
- [Contributing](./wiki/07-contributing/guide.md) — Development workflow
- [AGENTS.md](./AGENTS.md) — Agent instructions for this repository
```

#### 2. `wiki/llms.txt` (Wiki-Relative)

Same structure but with wiki-relative paths:

```markdown
# Project Name

> Comprehensive technical documentation for Project Name.

## Onboarding

- [Contributor Guide](./onboarding/contributor-guide.md)
- [Staff Engineer Guide](./onboarding/staff-engineer-guide.md)
- [Executive Guide](./onboarding/executive-guide.md)
- [Product Manager Guide](./onboarding/product-manager-guide.md)

## Architecture

- [Overview](./02-architecture/overview.md)
- [Data Flow](./02-architecture/data-flow.md)
- [API Design](./02-architecture/api-design.md)

... (same structure as root llms.txt)
```

#### 3. `wiki/llms-full.txt` (Full Inlined Content)

Inline full page content in `<doc>` blocks:

```markdown
<doc title="Project Name" path="./index.md">
---
title: Project Name — Documentation
description: Technical documentation for Project Name
---

# Project Name

Brief description...

## Quick Start

```bash
git clone <repo-url>
cd <repo>
npm install && npm run dev
```

## Architecture Overview

```mermaid
graph LR
  A --> B
```
<!-- Sources: src/app.ts:1 -->

... (full content, no frontmatter, preserve Mermaid and citations)
</doc>

<doc title="Getting Started" path="./01-getting-started/setup.md">
---
title: Setup
description: Installation and configuration
---

# Setup

Prerequisites table...

... (full content)
</doc>

... (one <doc> block per wiki page)
```

### Step 3: Create Public llms.txt

Copy to `wiki/.vitepress/public/llms.txt` for web access:

```bash
cp wiki/llms.txt wiki/.vitepress/public/llms.txt
```

### Requirements

- **Section order**: Onboarding → Architecture → Getting Started → Deep Dive → Optional
- **Optional section**: Content there can be skipped for shorter context windows
- **Link format**: Use relative Markdown links `[Text](./path/to/file.md)`
- **Full content**: Strip YAML frontmatter but preserve everything else
- **Preserve citations**: Keep all `[file:line](URL)` and `(file:line)` citations
- **Preserve diagrams**: Keep all Mermaid blocks and `<!-- Sources: ... -->` comments

### Validation

- All links should be relative and valid
- No duplicate `<doc>` blocks
- All wiki pages should be included
- Frontmatter should be stripped in full content
- Citations and diagrams should be preserved

$ARGUMENTS
