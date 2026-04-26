---
name: deep-wiki
description: AI-powered wiki generator for code repositories. Creates comprehensive documentation with dark-mode Mermaid diagrams, VitePress sites, onboarding guides, and LLM-friendly documentation. Use when you need to document a codebase, generate technical documentation, or create structured wikis.
---

# Deep Wiki - AI-Powered Documentation Generator

Generate comprehensive, structured, Mermaid-rich documentation wikis for any codebase with dark-mode VitePress sites, onboarding guides, and deep research capabilities.

## Setup

No setup required. The skill works out of the box.

## Usage

### Generate Full Wiki

```bash
/skill:deep-wiki generate
```

Generates a complete wiki with catalogue, all pages, onboarding guides, and VitePress site.

### Fast Wiki Generation

```bash
/skill:deep-wiki crisp
```

Generates a concise wiki (5-8 pages) optimized for speed and rate-limit avoidance.

### Single Page Generation

```bash
/skill:deep-wiki page "Authentication System"
```

Generates a single wiki page with dark-mode Mermaid diagrams and deep code citations.

### Research a Topic

```bash
/skill:deep-wiki research "How does the caching layer work?"
```

Conducts multi-turn deep research with evidence-based analysis.

### Generate Onboarding Guides

```bash
/skill:deep-wiki onboard
```

Creates 4 audience-tailored onboarding guides (Contributor, Staff Engineer, Executive, PM).

## Available Commands

| Command | Description |
|---------|-------------|
| `generate` | Full wiki generation with VitePress site |
| `crisp` | Fast, concise wiki generation |
| `catalogue` | Generate hierarchical JSON catalogue |
| `page <topic>` | Single page with diagrams |
| `research <topic>` | Deep research with 5 iterations |
| `ask <question>` | Q&A about the repository |
| `onboard` | 4 audience-tailored guides |
| `agents` | Generate AGENTS.md files |
| `llms` | Generate llms.txt files |
| `build` | Package as VitePress site |
| `deploy` | GitHub Pages deployment |
| `ado` | Azure DevOps conversion |

## Agents

The skill includes three specialized agents:

- **wiki-architect**: Analyzes repositories and generates structured catalogues
- **wiki-writer**: Creates rich documentation with dark-mode Mermaid diagrams
- **wiki-researcher**: Conducts evidence-based deep research

## Documentation

See the [full documentation](deep-wiki-plugin/README.md) for detailed usage instructions.

## Examples

```bash
# Generate full wiki for current repository
/skill:deep-wiki generate

# Research how authentication works
/skill:deep-wiki research "authentication flow"

# Create onboarding guides
/skill:deep-wiki onboard

# Build VitePress site
/skill:deep-wiki build
```

## Design Principles

1. **Source-linked citations**: All claims trace back to specific files and lines
2. **Evidence-based**: No hand-waving — every claim has code references
3. **Diagram-rich**: 3-5 Mermaid diagrams per page with dark-mode colors
4. **Table-driven**: Structured information in tables with Source columns
5. **Dark-mode native**: All output designed for dark-theme rendering
6. **Agent-discoverable**: Generates llms.txt and AGENTS.md for coding agents

## Requirements

- Git repository (for source citations)
- Node.js (for VitePress build)
- Optional: GitHub Pages (for deployment)
