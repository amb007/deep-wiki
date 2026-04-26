---
description: Generate 4 audience-tailored onboarding guides (Contributor, Staff Engineer, Executive, PM)
---

# Deep Wiki: Onboarding Guides

Generate four audience-tailored onboarding guides in an `onboarding/` folder.

## Process

### Step 1: Source Repository Resolution

1. Run `git remote get-url origin` to detect remote URL
2. Ask the user if not already provided: _"Source repo URL? (or 'local' for local-only citations)"_
3. Determine branch: `git rev-parse --abbrev-ref HEAD`
4. Store citation format:
   - **Remote**: `[file:line](REPO_URL/blob/BRANCH/file#Lline)`
   - **Local**: `(file:line)`

### Step 2: Detect Language & Framework

Scan for language indicators:
- `package.json` → JavaScript/TypeScript
- `*.csproj` → C#
- `Cargo.toml` → Rust
- `pyproject.toml` → Python
- `go.mod` → Go
- `*.sln` → .NET

### Step 3: Generate Guides

Create four guides with these specifications:

#### 1. Contributor Guide (1000–2500 lines)

**Audience**: New contributors (assumes Python/JS proficiency)

**Structure**:
- **Part I**: Language/framework foundations with cross-language comparisons
- **Part II**: This codebase's architecture and domain model
- **Part III**: Getting productive — setup, testing, contributing

**Content**:
- Glossary of domain terms
- Key files reference table
- Workflow diagrams (5+ Mermaid diagrams)
- Testing strategy and debug guide
- Contribution workflow

**Diagrams**: 5+ (architecture, workflow, data flow, class, sequence)

#### 2. Staff Engineer Guide (800–1200 lines)

**Audience**: Staff/principal engineers

**Structure**:
- System philosophy and core abstractions
- Key architectural decisions with tradeoff analysis
- Dependency rationale and versioning strategy
- Failure modes and mitigation strategies
- Performance characteristics and scaling limits

**Content**:
- Pseudocode in a DIFFERENT language (show understanding)
- Comparison tables (technologies, patterns, alternatives)
- THE ONE core architectural insight
- Design tradeoff discussion
- Decision log (key choices and rationale)

**Diagrams**: 5+ (architecture, class, sequence, state, ER)

#### 3. Executive Guide (400–800 lines)

**Audience**: VP/director-level engineering leaders

**Structure**:
- Capability map (what the system can do)
- Risk assessment (technical, operational, business)
- Technology investment thesis (why these choices)
- Cost/scaling model (infrastructure, maintenance)
- Actionable recommendations (3–5 concrete items)

**Content**:
- **NO code snippets** — service-level only
- Business impact analysis
- Roadmap considerations
- Team structure implications

**Diagrams**: 3+ (capability map, risk matrix, cost model)

#### 4. Product Manager Guide (400–800 lines)

**Audience**: Product managers and non-engineering stakeholders

**Structure**:
- User journey maps (how users interact with the system)
- Feature capability map (what's possible, what's not)
- Known limitations and workarounds
- Data/privacy overview (what's collected, how it's used)
- FAQ (common questions from stakeholders)

**Content**:
- **ZERO engineering jargon** — business language only
- User personas and scenarios
- Integration points with other systems
- Analytics and reporting capabilities

**Diagrams**: 3+ (user journey, capability map, data flow)

### Step 4: Create Hub Page

Generate `onboarding/index.md` with:
- Overview of available guides
- Audience selector (which guide is for whom)
- Links to all four guides
- Getting started recommendation

### Requirements

- **Minimum diagrams per guide**: Contributor/Staff (5+), Executive/PM (3+)
- **Dark-mode Mermaid**: fills `#2d333b`, borders `#6d5dfc`, text `#e6edf3`
- **Citations**: All claims linked to source files
- **Tables**: Use aggressively for structured information
- **No code snippets** in Executive/PM guides
- **No jargon** in PM guide

$ARGUMENTS
