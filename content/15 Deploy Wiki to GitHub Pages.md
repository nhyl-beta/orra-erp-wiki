---
tags: [orra-erp, deployment, quartz]
aliases: [Deploy Wiki, GitHub Pages]
---
# Deploying This Wiki with GitHub Pages

Up: [[00 Start Here]]

> [!summary]
> Step-by-step guide to deploy this Quartz wiki to GitHub Pages so it is accessible at `https://<username>.github.io/<repo-name>/`.

## Prerequisites
- Node.js v20+ and npm
- Git installed
- A GitHub account

## Steps

### Step 1: Install Quartz

```bash
git clone https://github.com/jackyzha0/quartz.git
cd quartz
npm i
```

### Step 2: Copy the wiki content

Copy all the `.md` files from this vault into `quartz/content/`:

```bash
# From the wiki output directory
cp -r content/* /path/to/quartz/content/
```

### Step 3: Configure Quartz

Edit `quartz.config.ts`:

```typescript
const config: QuartzConfig = {
  configuration: {
    pageTitle: "Orra-ERP Wiki",
    pageTitleSuffix: " | Orra-ERP",
    enableSPA: true,
    enablePopovers: true,
    analytics: null,
    locale: "en-US",
    baseUrl: "<username>.github.io/<repo-name>",
    ignorePatterns: ["private", "templates", ".obsidian"],
    defaultDateType: "modified",
    theme: {
      fontOrigin: "googleFonts",
      cdnCaching: true,
      typography: {
        header: "Space Grotesk",
        body: "Inter",
        code: "JetBrains Mono",
      },
      colors: {
        lightMode: {
          light: "#faf8f1",
          lightgray: "#e5e5e5",
          gray: "#b8b8b8",
          darkgray: "#4e4e4e",
          dark: "#2b2b2b",
          secondary: "#2d6a4f",
          tertiary: "#52b788",
          highlight: "rgba(45, 106, 79, 0.15)",
          textHighlight: "#fff23688",
        },
        darkMode: {
          light: "#161618",
          lightgray: "#393639",
          gray: "#646464",
          darkgray: "#d4d4d4",
          dark: "#ebebec",
          secondary: "#52b788",
          tertiary: "#74c69d",
          highlight: "rgba(82, 183, 136, 0.15)",
          textHighlight: "#fff23688",
        },
      },
    },
  },
  plugins: {
    transformers: [
      // defaults are fine for Obsidian wikilinks
    ],
    filters: [],
    emitters: [],
  },
}
```

### Step 4: Build the site

```bash
npx quartz build
```

This generates the static site in the `public/` directory.

### Step 5: Create a GitHub repository

```bash
# Create a new repo on GitHub (or use gh cli)
gh repo create <repo-name> --public --source=. --remote=origin
```

### Step 6: Set up GitHub Actions for deployment

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy Quartz to GitHub Pages

on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: actions/setup-node@v4
        with:
          node-version: 20

      - name: Install dependencies
        run: npm ci

      - name: Build Quartz
        run: npx quartz build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Step 7: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages**
3. Under **Source**, select **GitHub Actions**
4. Push your code to the `main` branch

```bash
git add .
git commit -m "Initial Quartz wiki deployment"
git push origin main
```

### Step 8: Access your wiki

After the GitHub Action completes (usually 1–2 minutes), your wiki will be live at:

```
https://<username>.github.io/<repo-name>/
```

## Updating the wiki

To update content:

1. Edit or add `.md` files in the `content/` directory
2. Commit and push to `main`
3. GitHub Actions rebuilds and redeploys automatically

```bash
git add content/
git commit -m "Update wiki content"
git push origin main
```

## Local preview

To preview changes before pushing:

```bash
npx quartz build --serve
```

Opens at `http://localhost:8080`.

## Troubleshooting

| Issue | Fix |
|---|---|
| Mermaid diagrams not rendering | Quartz v4 supports Mermaid natively; ensure you are on v4.4+ |
| Broken wikilinks | Quartz handles `[[...]]` links; ensure filenames match exactly |
| 404 on subpages | Check `baseUrl` in `quartz.config.ts` matches your repo name |
| Build fails on canvas files | `.canvas` files are Obsidian-specific; Quartz ignores them by default |
| Dark mode issues | Verify both `lightMode` and `darkMode` colour objects in config |

## Alternative: Deploy with `npx quartz sync`

Quartz has a built-in sync command that handles the GitHub setup:

```bash
npx quartz sync --no-pull
```

This pushes the built site to the `v4` branch and sets up GitHub Pages automatically. It is simpler but gives less control than the Actions workflow above.