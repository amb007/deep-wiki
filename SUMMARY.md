# Deep Wiki Skill - Installation Summary

## ✅ Successfully Ported and Packaged

The **Deep Wiki** plugin from Microsoft Skills has been successfully ported and packaged as a Pi Coding Agent skill.

## 📦 Package Structure

```
deep-wiki-skill/
├── SKILL.md              # Main skill definition (required)
├── package.json          # npm package metadata
├── README.md             # User documentation
├── INSTALL.md            # Installation instructions
├── PORTING.md            # Porting summary
├── SUMMARY.md            # This file
├── agents/
│   ├── wiki-architect.md
│   ├── wiki-writer.md
│   └── wiki-researcher.md
└── commands/
    ├── generate.md
    ├── crisp.md
    ├── catalogue.md
    ├── page.md
    ├── research.md
    ├── ask.md
    ├── onboard.md
    ├── changelog.md
    ├── agents.md
    ├── llms.md
    ├── build.md
    ├── deploy.md
    └── ado.md
```

## 🚀 Installation Options

### Option 1: Local Installation (Recommended)
```bash
# Copy to Pi global skills directory
cp -r ./deep-wiki-skill ~/.pi/agent/skills/deep-wiki

# Or copy to project skills directory
cp -r ./deep-wiki-skill .pi/skills/deep-wiki
```

### Option 2: npm Package Installation
```bash
# Install globally
npm install -g pi-deep-wiki

# Or install locally
npm install pi-deep-wiki
```

### Option 3: Settings Reference
```json
{
  "skills": ["./deep-wiki-skill"]
}
```

## 🎯 Usage

```bash
# Generate full wiki with VitePress site
/skill:deep-wiki generate

# Fast wiki generation (5-8 pages)
/skill:deep-wiki crisp

# Research a specific topic
/skill:deep-wiki research "How does authentication work?"

# Generate onboarding guides
/skill:deep-wiki onboard

# Build VitePress site
/skill:deep-wiki build

# Deploy to GitHub Pages
/skill:deep-wiki deploy
```

## 📚 What's Included

### 3 Specialized Agents
- **wiki-architect**: Analyzes repositories, generates structured catalogues
- **wiki-writer**: Creates rich documentation with dark-mode Mermaid diagrams
- **wiki-researcher**: Conducts evidence-based deep research

### 13 Commands
- `generate` - Full wiki generation
- `crisp` - Fast wiki generation
- `catalogue` - JSON TOC generation
- `page` - Single page generation
- `research` - Deep research (5 iterations)
- `ask` - Q&A about repository
- `onboard` - 4 audience-tailored guides
- `changelog` - Git-based changelog
- `agents` - AGENTS.md generation
- `llms` - llms.txt generation
- `build` - VitePress packaging
- `deploy` - GitHub Pages deployment
- `ado` - Azure DevOps conversion

## 🎨 Key Features

- **Source-linked citations**: Every claim traces to specific files/lines
- **Evidence-based**: No hand-waving, all claims have code references
- **Diagram-rich**: 3-5 Mermaid diagrams per page with dark-mode colors
- **Table-driven**: Structured information in tables with Source columns
- **Dark-mode native**: All output designed for dark-theme rendering
- **Agent-discoverable**: Generates llms.txt and AGENTS.md for coding agents

## 🔧 Requirements

- **Pi Coding Agent**: Latest version
- **Node.js**: Required for VitePress build (v20+ recommended)
- **Git**: Required for source repository citations
- **GitHub Pages**: Optional, for deployment

## 📝 Documentation

- [README.md](README.md) - Complete user guide
- [INSTALL.md](INSTALL.md) - Consolidated installation guide
- [PORTING.md](PORTING.md) - Porting details
- [agents/](agents/) - Agent definitions
- [commands/](commands/) - Command documentation

## 🎉 Next Steps

1. **Install the skill** using one of the methods above
2. **Verify installation** with `/skills list`
3. **Generate your first wiki** with `/skill:deep-wiki crisp`
4. **Explore advanced features** with `/skill:deep-wiki generate`

## 💡 Tips

- Start with `crisp` for fast results
- Use `research` for deep code analysis
- Generate `onboard` guides for new team members
- Use `build` and `deploy` for professional documentation sites

## 🔗 Original Source

Ported from: https://github.com/microsoft/skills/tree/main/.github/plugins/deep-wiki

## 📄 License

MIT License - Free to use, modify, and distribute

---

**The Deep Wiki skill is ready to use!** 🎉
Start documenting your codebases with AI-powered, evidence-based wiki generation.
