---
description: Generate GitHub Actions workflow to deploy wiki to GitHub Pages
---

# Deep Wiki: Deploy to GitHub Pages

Generate a GitHub Actions workflow to deploy the VitePress wiki to GitHub Pages.

## Process

### Step 1: Check for Existing Workflow

```bash
ls .github/workflows/deploy-wiki.yml 2>/dev/null
grep -rl "deploy-pages|pages-artifact" .github/workflows/ 2>/dev/null
```

If a pages workflow already exists, skip generation and report:
```
✅ GitHub Pages workflow already exists — skipping
```

### Step 2: Generate Workflow

Create `.github/workflows/deploy-wiki.yml`:

```yaml
name: Deploy Wiki to GitHub Pages

on:
  push:
    branches: [main, master]
    paths:
      - 'wiki/**'
      - '.github/workflows/deploy-wiki.yml'
  pull_request:
    branches: [main, master]
    paths:
      - 'wiki/**'
      - '.github/workflows/deploy-wiki.yml'

jobs:
  deploy:
    name: Deploy Wiki
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pages: write
      id-token: write
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 20

      - name: Install dependencies
        run: npm install
        working-directory: wiki

      - name: Build VitePress site
        run: npm run build
        working-directory: wiki

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: wiki/.vitepress/dist

      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Step 3: Configure GitHub Pages

Instruct the user to enable GitHub Pages:

```
## GitHub Pages Setup Required

> ⚠️ GitHub Pages requires manual enablement.

1. Go to **Repository Settings → Pages → Source**
2. Select **GitHub Actions** as the source
3. Without this, the workflow runs but the site won't publish

The site will be available at: `https://<username>.github.io/<repo>/`
```

### Step 4: Output Instructions

```
## Wiki Deployment Configured ✅

### What You Need To Do

1. **Commit the workflow:**
   ```bash
   git add .github/workflows/deploy-wiki.yml
   git commit -m "ci: add GitHub Pages deployment workflow"
   git push
   ```

2. **Enable GitHub Pages:**
   - Go to **Settings → Pages → Source → GitHub Actions**
   - Select the `github-pages` environment

3. **Access your wiki:**
   - After the workflow completes, visit: `https://<username>.github.io/<repo>/`
   - Or check the environment URL in the GitHub UI

### Workflow Details

- **Trigger**: Pushes to `main`/`master` that modify `wiki/` or the workflow file
- **Build**: Runs `npm install && npm run build` in the `wiki/` directory
- **Deploy**: Uses `actions/deploy-pages` to publish to GitHub Pages
- **Artifact**: Uploads `wiki/.vitepress/dist/` for deployment

### Customization

To customize the deployment:
- Change `branches` in `on.push` to match your default branch
- Add `concurrency` to prevent concurrent deployments
- Add cache for `node_modules` to speed up builds
```

### Requirements

- Repository must have GitHub Pages enabled
- Workflow needs `pages: write` and `id-token: write` permissions
- `wiki/.vitepress/config.mts` must have correct `base` path if not deploying to root

### Troubleshooting

**Site not deploying?**
- Check GitHub Pages source is set to "GitHub Actions"
- Verify the workflow has the correct permissions
- Check the Actions tab for build errors

**404 after deployment?**
- Ensure `base` in VitePress config matches your repo name: `base: '/repo-name/'`
- For user/organization pages, use `base: '/'`

**Build failures?**
- Run `npm install && npm run build` locally in `wiki/` to debug
- Check Node.js version compatibility (workflow uses v20)

$ARGUMENTS
