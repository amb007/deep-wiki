# 🌊 Deep Wiki

**AI-Powered Wiki Generator for Code Repositories — Ported for Pi Coding Agent**

Generate comprehensive, structured, Mermaid-rich documentation wikis for any codebase — with dark-mode VitePress sites, onboarding guides, and deep research capabilities. Distilled from the prompt architectures of [OpenDeepWiki](https://github.com/AIDotNet/OpenDeepWiki) and [deepwiki-open](https://github.com/AsyncFuncAI/deepwiki-open).

## Installation

This plugin is ported for use with the Pi Coding Agent. Place it in your working directory and use the commands directly.

```bash
# Clone or copy this deep-wiki directory to your project
cp -r ./deep-wiki /path/to/your/project/.pi-plugins/deep-wiki
```

## Commands

| Command | Description |
|---------|-------------|
| `/skill:deep-wiki generate` | Generate a complete wiki — catalogue + all pages + onboarding guides + VitePress site |
| `/skill:deep-wiki crisp` | Fast wiki generation — concise, parallelized, rate-limit-friendly. 5–8 pages, no build step |
| `/skill:deep-wiki catalogue` | Generate only the hierarchical wiki structure as JSON |
| `/skill:deep-wiki page <topic>` | Generate a single wiki page with dark-mode Mermaid diagrams |
| `/skill:deep-wiki changelog` | Generate a structured changelog from git commits |
| `/skill:deep-wiki research <topic>` | Multi-turn deep investigation with evidence-based analysis |
| `/skill:deep-wiki ask <question>` | Ask a question about the repository |
| `/skill:deep-wiki onboard` | Generate 4 audience-tailored onboarding guides (Contributor, Staff Engineer, Executive, PM) |
| `/skill:deep-wiki agents` | Generate `AGENTS.md` files for pertinent folders (only where missing) |
| `/skill:deep-wiki llms` | Generate `llms.txt` and `llms-full.txt` for LLM-friendly project access |
| `/skill:deep-wiki ado` | Generate a Node.js script to convert wiki to Azure DevOps Wiki-compatible format |
| `/skill:deep-wiki build` | Package generated wiki as a VitePress site with dark theme |
| `/skill:deep-wiki deploy` | Generate GitHub Actions workflow to deploy wiki to GitHub Pages |

## Agents

| Agent | Description |
|-------|-------------|
| `wiki-architect` | Analyzes repos, generates structured catalogues + onboarding architecture |
| `wiki-writer` | Generates pages with dark-mode Mermaid diagrams and deep citations |
| `wiki-researcher` | Deep research with zero tolerance for shallow analysis — evidence-first |

## Quick Start

```bash
# Generate a full wiki with onboarding guides and VitePress site
/skill:deep-wiki generate

# Fast wiki — concise, parallelized, avoids rate limits
/skill:deep-wiki crisp

# Just the structure
/skill:deep-wiki catalogue

# Single page with dark-mode diagrams
/skill:deep-wiki page Authentication System

# Generate onboarding guides
/skill:deep-wiki onboard

# Build VitePress dark-theme site
/skill:deep-wiki build

# Research a topic (evidence-based, 5 iterations)
/skill:deep-wiki research How does the caching layer work?

# Ask a question
/skill:deep-wiki ask What database migrations exist?

# Generate llms.txt for LLM-friendly access
/skill:deep-wiki llms

# Deploy wiki to GitHub Pages (optional)
/skill:deep-wiki deploy
```

## How It Works

```
Repository → Scan → Catalogue (JSON TOC) → Per-Section Pages → Assembled Wiki
                                                    ↓
                                         Mermaid Diagrams + Citations
                                                    ↓
                                         Onboarding Guides (Contributor, Staff Engineer, Executive, PM)
                                                    ↓
                                         VitePress Site (Dark Theme + Click-to-Zoom)
                                                    ↓
                                         AGENTS.md Files (Only If Missing)
                                                    ↓
                                         llms.txt + llms-full.txt (LLM-friendly)
                                                    ↓
                                         GitHub Pages Deployment (Optional)
```

| Step | Component | What It Does |
|------|-----------|-------------|
| 1 | `wiki-architect` | Analyzes repo → hierarchical JSON table of contents |
| 2 | `wiki-page-writer` | For each TOC entry → rich Markdown with dark-mode Mermaid + citations |
| 3 | `wiki-onboarding` | Generates 4 audience-tailored onboarding guides in `onboarding/` folder |
| 4 | `wiki-vitepress` | Packages all pages into a VitePress dark-theme static site |
| 5 | `wiki-changelog` | Git commits → categorized changelog |
| 6 | `wiki-researcher` | Multi-turn investigation with evidence standard |
| 7 | `wiki-qa` | Q&A grounded in actual source code |
| 8 | `wiki-agents-md` | Generates `AGENTS.md` files for pertinent folders (only if missing) |
| 9 | `wiki-llms-txt` | Generates `llms.txt` + `llms-full.txt` for LLM-friendly access |
| 10 | `wiki-ado-convert` | Converts VitePress wiki to Azure DevOps Wiki-compatible format |

## Design Principles

1. **Source-linked citations**: Before any task, resolve the source repo URL (or confirm local). All citations use `[file:line](REPO_URL/blob/BRANCH/file#Lline)` for remote repos, `(file:line)` for local
2. **Structure-first**: Always generate a TOC/catalogue before page content
3. **Evidence-based**: Every claim cites `file_path:line_number` with clickable links — no hand-waving
4. **Diagram-rich**: Minimum 3–5 dark-mode Mermaid diagrams per page using multiple diagram types, with click-to-zoom and `<!-- Sources: ... -->` comment blocks. More diagrams = better — use them liberally for architecture, flows, state, data models, and decisions.
5. **Table-driven**: Prefer tables over prose for any structured information. Use summary tables, comparison tables, and always include a "Source" column with citations.
6. **Progressive disclosure**: Big picture first, then drill into details. Every section starts with a TL;DR.
7. **Hierarchical depth**: Max 4 levels for component-level granularity
8. **Systems thinking**: Architecture → Subsystems → Components → Methods
9. **Never invent**: All content derived from actual code — trace real implementations
10. **Dark-mode native**: All output designed for dark-theme rendering (VitePress)
11. **Depth before breadth**: Trace actual code paths, never guess from file names
12. **Agent-discoverable**: Output placed at standard paths (`llms.txt` at repo root, `AGENTS.md` in key folders) so coding agents and MCP tools find documentation automatically

## Agent & MCP Integration

The generated output is designed to be discoverable by coding agents using the Pi Coding Agent framework:

| File | Path | Discovery Method |
|------|------|-----------------|
| `llms.txt` | Repo root (`./llms.txt`) | Standard llms.txt spec location — agents check here first via file reading
| `llms-full.txt` | `wiki/llms-full.txt` | Full inlined docs — agents load this for comprehensive context
| `AGENTS.md` | Root + key folders | Standard agent instructions file — references wiki docs in Documentation section
| Wiki pages | `wiki/**/*.md` | Searchable via file search — all pages contain source-linked citations
| `llms.txt` | `wiki/.vitepress/public/` | Served at `/llms.txt` on deployed VitePress site

**How it works with Pi Coding Agent:**

1. Agent reads `llms.txt` → gets project summary + links to all wiki pages
2. Agent reads specific wiki pages → gets full documentation with source citations
3. Agent searches for patterns → finds relevant wiki sections across the repository
4. Agent reads `AGENTS.md` → Documentation section points to wiki and onboarding guides

## Plugin Structure

```
deep-wiki/
├── agents/
│   ├── wiki-architect.md
│   ├── wiki-writer.md
│   └── wiki-researcher.md
├── commands/
│   ├── generate.md
│   ├── crisp.md
│   ├── catalogue.md
│   ├── page.md
│   ├── changelog.md
│   ├── research.md
│   ├── ask.md
│   ├── onboard.md
│   ├── agents.md
│   ├── llms.md
│   ├── ado.md
│   ├── build.md
│   └── deploy.md
└── README.md
```

## License

MIT
