---
description: Generate a Node.js script to convert wiki to Azure DevOps Wiki-compatible format
---

# Deep Wiki: Azure DevOps Wiki Conversion

Generate a Node.js script to convert the VitePress wiki to Azure DevOps Wiki-compatible format.

## Process

### Step 1: Generate Conversion Script

Create `scripts/convert-to-ado-wiki.js`:

```javascript
#!/usr/bin/env node

/**
 * Convert VitePress wiki to Azure DevOps Wiki format
 * 
 * Azure DevOps Wiki uses a different Markdown dialect:
 * - No YAML frontmatter
 * - Different Mermaid syntax (some features not supported)
 * - Different table formatting
 * - No HTML comments
 */

import fs from 'fs/promises'
import path from 'path'
import { glob } from 'glob'

const WIKI_DIR = './wiki'
const ADO_WIKI_DIR = './ado-wiki'

async function convert() {
  // Create output directory
  await fs.mkdir(ADO_WIKI_DIR, { recursive: true })

  // Get all markdown files (excluding .vitepress and node_modules)
  const files = await glob('**/*.md', {
    cwd: WIKI_DIR,
    ignore: ['**/node_modules/**', '**/.vitepress/**', '**/.vitepress/**']
  })

  console.log(`Found ${files.length} markdown files to convert`)

  for (const file of files) {
    const inputPath = path.join(WIKI_DIR, file)
    const outputPath = path.join(ADO_WIKI_DIR, file)
    
    // Ensure output directory exists
    await fs.mkdir(path.dirname(outputPath), { recursive: true })
    
    const content = await fs.readFile(inputPath, 'utf8')
    let converted = content

    // 1. Remove YAML frontmatter
    converted = converted.replace(/^---\s*[\s\S]*?---\s*/, '')

    // 2. Convert Mermaid diagrams (simplify for ADO compatibility)
    converted = converted.replace(
      /```mermaid\s*([\s\S]*?)\s*```/g,
      (match, diagram) => {
        // Remove inline styles (ADO has limited Mermaid support)
        let adoDiagram = diagram.replace(/style\s+\w+\s+fill:#[\w]+,stroke:#[\w]+,color:#[\w]+/g, '')
        // Remove HTML comments
        adoDiagram = adoDiagram.replace(/<!--[\s\S]*?-->/g, '')
        // Remove autonumber (not supported in ADO)
        adoDiagram = adoDiagram.replace(/autonumber\s*,?/g, '')
        return `\`\`\`mermaid\n${adoDiagram.trim()}\n\`\`\`
      }
    )

    // 3. Remove HTML comments (ADO doesn't support them)
    converted = converted.replace(/<!--[\s\S]*?-->/g, '')

    // 4. Fix table formatting (ADO is picky about tables)
    converted = converted.replace(
      /\|\s*([^|]+)\s*\|\s*([^|]+)\s*\|/g,
      '| $1 | $2 |'
    )

    // 5. Write converted file
    await fs.writeFile(outputPath, converted)
    console.log(`✅ Converted: ${file}`)
  }

  console.log('\n🎉 Conversion complete!')
  console.log(`Output directory: ${ADO_WIKI_DIR}`)
  console.log('\nNext steps:')
  console.log('1. Review the converted files in ado-wiki/')
  console.log('2. Manually upload to Azure DevOps Wiki or use the API')
  console.log('3. Check diagrams render correctly in ADO')
}

convert().catch(console.error)
```

### Step 2: Generate Package JSON

Create `scripts/package.json`:

```json
{
  "name": "ado-wiki-converter",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "convert": "node convert-to-ado-wiki.js"
  },
  "dependencies": {
    "glob": "^10.3.10"
  }
}
```

### Step 3: Output Instructions

```
## Azure DevOps Wiki Conversion Generated ✅

### Files Created

- `scripts/convert-to-ado-wiki.js` — Conversion script
- `scripts/package.json` — Node.js project

### How to Use

1. **Install dependencies:**
   ```bash
   cd scripts && npm install
   ```

2. **Run conversion:**
   ```bash
   npm run convert
   ```

3. **Review output:**
   - Converted files are in `ado-wiki/`
   - Check that diagrams and tables render correctly

### What Gets Converted

| Element | Conversion |
|---------|------------|
| YAML frontmatter | Removed (ADO doesn't support it) |
| Mermaid diagrams | Simplified for ADO compatibility |
| HTML comments | Removed (ADO doesn't support them) |
| Tables | Reformatted for ADO compatibility |
| Links | Preserved as-is |
| Code blocks | Preserved as-is |

### Limitations

**Azure DevOps Wiki has limited Mermaid support:**
- No inline styles (removed)
- No `autonumber` in sequence diagrams (removed)
- Limited diagram types (stick to basic graphs, sequence, class)
- No subgraphs in some cases

**Manual adjustments may be needed:**
- Complex diagrams might need simplification
- Some Mermaid features aren't supported
- Table formatting might need tweaks

### Uploading to Azure DevOps

You have two options:

**Option 1: Manual Upload**
1. Go to your Azure DevOps project
2. Navigate to Wiki → Pages
3. Click "Upload file" and select files from `ado-wiki/`

**Option 2: API Upload**
Use the [Azure DevOps Wiki API](https://learn.microsoft.com/en-us/rest/api/azure/devops/wiki/) to automate uploads.

### Alternative: Use as Reference

Instead of converting, you can:
1. Keep the VitePress wiki as the source of truth
2. Link to it from Azure DevOps
3. Use the wiki for comprehensive documentation
4. Use ADO Wiki for ADO-specific notes only
```

### Requirements

- Node.js 18+ for running the conversion script
- Azure DevOps project with Wiki enabled
- Manual review of converted content

$ARGUMENTS
