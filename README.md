# GitHub Pages Deployment

## How to Enable

1. **Push this `docs/` folder to your GitHub repo** (e.g., `xai-liacs/llamea`)

2. **Enable GitHub Pages:**
   - Go to repo **Settings → Pages**
   - Under "Source", select **Deploy from a branch**
   - Select the **main** branch and **/docs** folder
   - Click **Save**

3. **Wait 1-2 minutes** for deployment, then your wiki will be live at:
   `https://xai-liacs.github.io/llamea/` (or your actual org/repo)

## Local Development

To preview locally:

```bash
cd docs
npx docsify-cli serve .
```

Or use any static server:

```bash
cd docs
python3 -m http.server 3000
```

Then open http://localhost:3000

## Customization

- Edit `_sidebar.md` to change navigation
- Edit `index.html` to change theme/config
- Edit `pages/*.md` for content changes

## Notes

- Files starting with `_` are ignored by docsify routing
- `.nojekyll` file prevents GitHub Jekyll processing
- Uses Docsify loaded from CDN (no build step needed)
