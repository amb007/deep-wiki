# Deep Wiki Plugin Porting Summary

## Overview

This document describes how the Deep Wiki plugin from Microsoft Skills was ported for use with the Pi Coding Agent.

## Source

Original plugin: https://github.com/microsoft/skills/tree/main/.github/plugins/deep-wiki

## Changes Made

### 1. Structure Conversion

**Original Structure:**
```
.github/plugins/deep-wiki/
├── .claude-plugin/
├── agents/
├── commands/
├── skills/
└── README.md
```

**Ported Structure:**
```
deep-wiki-skill/
├── SKILL.md              # Main skill definition
├── package.json          # npm package metadata
├── README.md             # User documentation
├── INSTALL.md            # Installation instructions
├── PORTING.md            # This file
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

### 2. Skill Adaptation

**Original:** Claude plugin format with `.claude-plugin/plugin.json`

**Ported:** Pi Coding Agent skill format with `SKILL.md` following the [Agent Skills specification](https://agentskills.io/specification)

### 3. Key Adaptations

1. **Removed Claude-specific files:**
   - `.claude-plugin/` directory
   - Claude-specific metadata

2. **Added Pi-specific files:**
   - `SKILL.md` with proper frontmatter
   - `package.json` for npm installation
   - Installation documentation

3. **Preserved all functionality:**
   - All 3 agents (architect, writer, researcher)
   - All 13 commands
   - All design principles and requirements

### 4. Command Format

**Original:** `/deep-wiki:command`

**Ported:** `/skill:deep-wiki command`

## Installation Methods

### 1. Local Copy
```bash
cp -r deep-wiki-skill ~/.pi/agent/skills/deep-wiki
```

### 2. npm Package
```bash
npm install -g pi-deep-wiki
```

### 3. Settings Reference
```json
{
  "skills": ["./deep-wiki-skill"]
}
```

## Usage Examples

```bash
# Generate full wiki
/skill:deep-wiki generate

# Fast wiki generation
/skill:deep-wiki crisp

# Research a topic
/skill:deep-wiki research "authentication system"

# Generate onboarding guides
/skill:deep-wiki onboard
```

## Compatibility

### Pi Coding Agent Requirements
- Version: Latest (tested with current release)
- Node.js: Required for VitePress build
- Git: Required for source citations

### Browser/Environment
- Works in all Pi-supported environments
- VitePress build requires Node.js environment

## Testing

The ported skill has been verified to:
- ✅ Follow Agent Skills specification
- ✅ Include all original functionality
- ✅ Maintain proper skill structure
- ✅ Support all installation methods
- ✅ Preserve all documentation and examples

## Future Enhancements

Potential improvements for the Pi version:
- Add Pi-specific examples in documentation
- Create Pi-themed templates
- Add Pi agent integration examples
- Create demo videos for Pi usage

## License

MIT License (same as original)

## Credits

- Original: Microsoft Skills team
- Porting: Pi Coding Agent adaptation
- Based on: OpenDeepWiki and deepwiki-open architectures
