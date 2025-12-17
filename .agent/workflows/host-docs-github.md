---
description: How to host docs on GitHub Pages
---

# Host Documentation on GitHub Pages

Follow these steps to host your `docs.html` file on GitHub Pages:

## Step 1: Prepare the documentation structure

// turbo-all

Choose one of these options:

### Option A: Use /docs folder (Recommended)
```bash
mkdir docs
copy docs.html docs\index.html
```

### Option B: Use root with index.html
```bash
copy docs.html index.html
```

## Step 2: Commit and push your changes

```bash
git add .
git commit -m "Add documentation for GitHub Pages"
git push origin main
```

## Step 3: Enable GitHub Pages

1. Go to your GitHub repository in a browser
2. Click **Settings** tab
3. Click **Pages** in the left sidebar
4. Under "Source":
   - Select branch: **main**
   - Select folder: **/docs** (if using Option A) or **/ (root)** (if using Option B)
5. Click **Save**

## Step 4: Wait for deployment

- GitHub Pages will take 1-3 minutes to deploy
- You'll see a message: "Your site is published at https://username.github.io/repo-name/"

## Step 5: Access your documentation

Your documentation will be available at:
- **Option A (docs folder)**: `https://username.github.io/repo-name/`
- **Option B (root)**: `https://username.github.io/repo-name/` or `https://username.github.io/repo-name/index.html`
- **If kept as docs.html in root**: `https://username.github.io/repo-name/docs.html`

## Troubleshooting

- **404 Error**: Make sure your branch and folder settings are correct
- **Not updating**: Try clearing browser cache or wait a few minutes
- **Custom domain**: You can add a custom domain in Settings → Pages → Custom domain
