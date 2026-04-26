# Deep Wiki Skill Installation

## Installation Methods

### Method 1: Local Installation (Recommended)

Copy the skill to your Pi skills directory:

```bash
# Copy to global skills directory
cp -r ./deep-wiki-skill ~/.pi/agent/skills/deep-wiki

# Or copy to project skills directory
cp -r ./deep-wiki-skill .pi/skills/deep-wiki
```

### Method 2: Package Manager Installation

Install as a package using npm, yarn, pnpm, or bun:

#### npm
```bash
# Install globally
npm install -g pi-deep-wiki

# Or install locally in your project
npm install pi-deep-wiki
```

#### yarn
```bash
# Install globally
yarn global add pi-deep-wiki

# Or install locally in your project
yarn add pi-deep-wiki
```

#### pnpm
```bash
# Install globally
pnpm add -g pi-deep-wiki

# Or install locally in your project
pnpm add pi-deep-wiki
```

#### bun (Recommended - Fastest)
```bash
# Install globally
bun add -g pi-deep-wiki

# Or install locally in your project
bun add pi-deep-wiki
```

After package installation, Pi will automatically discover the skill from the `node_modules` package.

### Method 3: Direct Path Reference

Add the skill path to your Pi settings:

```json
{
  "skills": ["./deep-wiki-skill"]
}
```

## Verification

Check that the skill is loaded:

```bash
/skills list
```

You should see `deep-wiki` in the list of available skills.

## Usage

Once installed, use the skill with:

```bash
/skill:deep-wiki generate
/skill:deep-wiki research "topic"
/skill:deep-wiki onboard
```

## Uninstallation

### Local Installation

```bash
rm -rf ~/.pi/agent/skills/deep-wiki
# or
rm -rf .pi/skills/deep-wiki
```

### npm Installation

```bash
npm uninstall -g pi-deep-wiki
# or
npm uninstall pi-deep-wiki
```

### Settings Reference

Remove from `settings.json`:

```json
{
  "skills": []
}
```

## Troubleshooting

**Skill not showing up?**
- Check the skill name matches the directory name (`deep-wiki`)
- Verify `SKILL.md` has proper frontmatter
- Check Pi logs for skill loading errors

**Commands not working?**
- Ensure you're using `/skill:deep-wiki command` format
- Check that skill commands are enabled in settings
# Complete Installation Guide

## 📋 Installation Methods Summary

Choose the method that best fits your workflow:

## 🚀 Quick Start (Recommended)

```bash
# Copy to Pi skills directory
cp -r ./deep-wiki-skill ~/.pi/agent/skills/deep-wiki

# Or install via package manager
bun add -g pi-deep-wiki
```

## 📂 Local Installation

### Method 1: Direct Copy

```bash
# Copy to global skills directory
cp -r ./deep-wiki-skill ~/.pi/agent/skills/deep-wiki

# Or copy to project skills directory
cp -r ./deep-wiki-skill .pi/skills/deep-wiki
```

**Pros:** Simple, no dependencies, immediate access
**Cons:** Manual updates

### Method 2: Git Clone

```bash
git clone https://github.com/amb007/pi-deep-wiki.git ~/.pi/agent/skills/deep-wiki
```

**Pros:** Easy to update with `git pull`
**Cons:** Requires git

## 📦 Package Manager Installation

### Method 3: bun (Recommended - Fastest)

```bash
# Install bun first
curl -fsSL https://bun.sh/install | bash

# Install skill
bun add -g pi-deep-wiki
```

**Pros:** Fastest installation, modern tooling
**Cons:** Requires bun installation

### Method 4: npm

```bash
npm install -g pi-deep-wiki
```

**Pros:** Widely supported, familiar
**Cons:** Slower than bun

### Method 5: yarn

```bash
yarn global add pi-deep-wiki
```

**Pros:** Good for yarn workflows
**Cons:** Requires yarn

### Method 6: pnpm

```bash
pnpm add -g pi-deep-wiki
```

**Pros:** Efficient, fast
**Cons:** Requires pnpm

## 📝 Settings Reference

Add to `.pi/settings.json`:

```json
{
  "skills": [
    "./deep-wiki-skill",
    "amb007/pi-deep-wiki"
  ]
}
```

**Pros:** Flexible, multiple locations
**Cons:** Requires file editing

## 🔧 Verification

After installation, verify the skill is working:

```bash
# Check skill is loaded
/skills list

# Should see "deep-wiki" in the list

# Test a command
/skill:deep-wiki generate
```

## 📊 Comparison Table

| Method | Command | Speed | Updates | Dependencies |
|--------|---------|-------|---------|--------------|
| **Direct Copy** | `cp -r` | ⚡ Instant | Manual | None |
| **Git Clone** | `git clone` | 🏎 Fast | `git pull` | git |
| **bun** | `bun add -g` | ⚡ Fastest | `bun upgrade` | bun |
| **npm** | `npm install -g` | 🐢 Slow | `npm update` | node/npm |
| **yarn** | `yarn global add` | 🏎 Fast | `yarn upgrade` | yarn |
| **pnpm** | `pnpm add -g` | 🚀 Fast | `pnpm update` | pnpm |
| **Settings** | Edit JSON | ⚡ Instant | Manual | None |

## 🎯 Recommendation

**For most users:** Direct copy or bun
- Simple projects → `cp -r`
- Existing bun users → `bun add -g`
- Team projects → Git clone
- npm workflows → `npm install -g`

## 📚 Related Files

- [INSTALL.md](./INSTALL.md) - Detailed installation
- [BUN-INSTALL.md](./BUN-INSTALL.md) - Bun-specific guide

## 🔗 Quick Links

- **GitHub:** https://github.com/amb007/pi-deep-wiki
- **npm:** https://www.npmjs.com/package/pi-deep-wiki
- **Documentation:** https://github.com/amb007/pi-deep-wiki#readme

Choose your preferred method and get started with Deep Wiki! 🎉
# Bun Installation Guide

## 🐇 Bun Package Manager

Bun is a fast, modern JavaScript runtime and package manager that's compatible with npm packages.

## 🚀 Installing with Bun

### 1. Install Bun (if not already installed)

```bash
# Install bun globally
curl -fsSL https://bun.sh/install | bash

# Or with npm
npm install -g bun

# Verify installation
bun --version
```

### 2. Install Deep Wiki Skill

```bash
# Install globally (recommended)
bun add -g pi-deep-wiki

# Or install locally in your project
bun add pi-deep-wiki
```

### 3. Verify Installation

```bash
# Check package is installed
bun list -g | grep pi-deep-wiki

# Check skill is discoverable
ls ~/.bun/install/global/node_modules/pi-deep-wiki/SKILL.md
```

## 🎯 Why Use Bun?

| Feature | Bun | npm | yarn | pnpm |
|---------|-----|-----|------|------|
| **Speed** | ⚡ Fastest | 🐢 Slow | ⏳ Medium | 🏎 Fast |
| **Compatibility** | ✅ npm compatible | ✅ Standard | ✅ Standard | ✅ Standard |
| **Installation** | `bun add` | `npm install` | `yarn add` | `pnpm add` |
| **Global install** | `bun add -g` | `npm install -g` | `yarn global add` | `pnpm add -g` |
| **Lockfile** | `bun.lockb` | `package-lock.json` | `yarn.lock` | `pnpm-lock.yaml` |

## 📚 Usage with Pi Coding Agent

After installing with Bun, Pi will automatically discover the skill:

```bash
# The skill should be available as
/skill:deep-wiki generate
/skill:deep-wiki research "topic"
/skill:deep-wiki onboard
```

## 🔧 Troubleshooting

### Bun not found

```bash
# Reinstall bun
curl -fsSL https://bun.sh/install | bash

# Add to PATH
export PATH="$HOME/.bun/bin:$PATH"
```

### Package not found

```bash
# Check bun registry
bun config get registry

# Ensure it's set to npm registry
bun config set registry https://registry.npmjs.org/
```

### Permission issues

```bash
# Use sudo if needed
sudo bun add -g pi-deep-wiki

# Or fix permissions
mkdir -p ~/.bun/bin
chown -R $USER ~/.bun
```

## 📋 Comparison

### Installation Speed

```bash
# Bun (fastest)
time bun add pi-deep-wiki

# npm (slowest)
time npm install pi-deep-wiki

# pnpm (fast)
time pnpm add pi-deep-wiki
```

### Command Comparison

| Action | Bun | npm | yarn | pnpm |
|--------|-----|-----|------|------|
| Install | `bun add` | `npm install` | `yarn add` | `pnpm add` |
| Global | `bun add -g` | `npm install -g` | `yarn global add` | `pnpm add -g` |
| Remove | `bun remove` | `npm uninstall` | `yarn remove` | `pnpm remove` |
| Update | `bun update` | `npm update` | `yarn upgrade` | `pnpm update` |
| Run | `bun run` | `npm run` | `yarn run` | `pnpm run` |

## 🎉 Recommendation

**Use Bun if:**
- You want the fastest installation
- You're already using Bun for other projects
- You want modern JavaScript tooling

**Use npm/yarn/pnpm if:**
- You're already using those in your project
- You need specific features from those package managers
- You have existing workflows

## 📚 Related Files

- [INSTALL.md](./INSTALL.md) - General installation guide
- [package.json](./package.json) - Package configuration

## 🔗 References

- Bun Website: https://bun.sh/
- Bun GitHub: https://github.com/oven-sh/bun
- Bun Documentation: https://bun.sh/docs

Bun provides a **fast, modern alternative** to npm while maintaining full compatibility! 🚀
