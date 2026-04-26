---
description: Generate AGENTS.md files for pertinent folders (only where missing)
---

# Deep Wiki: AGENTS.md Generation

Generate `AGENTS.md` files for pertinent repository folders to provide coding agents with project-specific context.

## Process

### Step 1: Source Repository Resolution

1. Run `git remote get-url origin` to detect remote URL
2. Ask the user if not already provided: _"Source repo URL? (or 'local' for local-only citations)"_
3. Determine branch: `git rev-parse --abbrev-ref HEAD`
4. Store citation format:
   - **Remote**: `[file:line](REPO_URL/blob/BRANCH/file#Lline)`
   - **Local**: `(file:line)`

### Step 2: Identify Pertinent Folders

Scan for folders that need AGENTS.md:
- Repository root
- `wiki/` (if generated)
- `tests/`
- `src/`
- `lib/`
- `app/`
- `packages/*/`
- `services/*/`
- Any folder with build manifest (`package.json`, `pyproject.toml`, etc.)

### Step 3: Generate AGENTS.md Files

**CRITICAL: NEVER overwrite existing AGENTS.md files.**

For each folder:
1. Check if `AGENTS.md` exists
2. If YES → skip and report: `"✅ AGENTS.md already exists — skipping"`
3. If NO → generate tailored AGENTS.md

### AGENTS.md Structure

```markdown
# Agent Instructions for [Folder Name]

## Build & Run Commands (MUST READ FIRST)

```bash
# Install dependencies
npm install

# Run development server
npm run dev

# Build for production
npm run build
```

## Testing

```bash
# Run tests
npm test

# Run tests with coverage
npm run test:coverage
```

## Project Structure

```
folder/
├── src/          # Source code
├── tests/        # Test files
├── config/       # Configuration
└── package.json  # Build manifest
```

## Code Style

- Use TypeScript with strict mode
- Follow Prettier formatting
- Use ESLint for linting
- Document public APIs with JSDoc

## Git Workflow

- Main branch: `main`
- Feature branches: `feature/*`
- PR process: Requires 2 approvals
- Commit style: Conventional Commits

## Boundaries

| Action | Rule |
|--------|------|
| Modify build config | ⚠️ Ask first |
| Add new dependencies | ✅ Always OK |
| Change API contracts | 🚫 Never without discussion |
| Refactor internal code | ✅ Always OK |

## Documentation

- [Wiki](../../wiki/) — Full documentation
- [Onboarding Guides](../../wiki/onboarding/) — Getting started
- [llms.txt](../../llms.txt) — LLM-friendly summary
- [llms-full.txt](../../wiki/llms-full.txt) — Full inlined docs
```

### Step 4: Generate CLAUDE.md Companions

For each folder where AGENTS.md was created (and CLAUDE.md doesn't exist):

```markdown
# Claude Agent Instructions

<!-- Generated file — do not edit directly -->

> 📖 **Please read** `AGENTS.md` for project-specific instructions.
```

### Step 5: Wiki AGENTS.md (Special Case)

If `wiki/` folder exists and doesn't have `AGENTS.md`:

```markdown
# Agent Instructions for Wiki

## Build & Run Commands

```bash
# Install VitePress dependencies
npm install

# Run dev server (http://localhost:5173)
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## Wiki Structure

```
wiki/
├── index.md                      # Landing page
├── onboarding/                   # Onboarding guides
│   ├── contributor-guide.md      # For new contributors
│   ├── staff-engineer-guide.md   # For staff engineers
│   ├── executive-guide.md        # For engineering leaders
│   └── product-manager-guide.md  # For PMs
├── 01-getting-started/           # Setup and basics
├── 02-architecture/              # System design
├── ...                            # Other sections
├── llms.txt                       # LLM-friendly links
├── llms-full.txt                  # Full inlined content
└── .vitepress/                    # VitePress config
```

## Content Conventions

- **Mermaid diagrams**: Use dark-mode colors (`fill:#2d333b`, `stroke:#6d5dfc`, `color:#e6edf3`)
- **Citations**: Link to source files with `[file:line](REPO_URL/blob/BRANCH/file#Lline)`
- **Frontmatter**: Include `title`, `description`, `outline: deep` in every page
- **Diagram sources**: Add `<!-- Sources: file:line, file:line -->` after every Mermaid block

## Boundaries

| Action | Rule |
|--------|------|
| Delete generated pages | 🚫 Never |
| Modify theme CSS | ⚠️ Test thoroughly |
| Add new pages | ✅ Always OK |
| Update existing pages | ✅ Always OK |

## Documentation

- [llms.txt](./llms.txt) — LLM-friendly wiki links
- [llms-full.txt](./llms-full.txt) — Full inlined content
- [VitePress Docs](https://vitepress.dev/) — VitePress reference
```

### Step 6: Output Summary

Report which files were:
- Created (list paths)
- Skipped (already exist)
- Not applicable (no build manifest)

### Requirements

- **NEVER overwrite** existing AGENTS.md or CLAUDE.md
- **Root AGENTS.md** covers whole project
- **Nested AGENTS.md** covers folder-specific details only
- **Wiki AGENTS.md** covers VitePress site specifics
- **Always reference** llms.txt and llms-full.txt in Documentation section

$ARGUMENTS
