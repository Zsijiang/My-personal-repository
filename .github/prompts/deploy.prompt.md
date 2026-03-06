---
mode: 'agent'
description: 'Render Quarto slides and sync to docs/ for GitHub Pages deployment. Use when deploying lecture slides after making changes.'
---

# Deploy Slides to GitHub Pages

Render Quarto slides and sync all files to `docs/` for GitHub Pages deployment.

## Steps

1. **Run the sync script:**
   - If a lecture name is provided (e.g., "Lecture4"): `./scripts/sync_to_docs.sh Lecture4`
   - If no argument: `./scripts/sync_to_docs.sh` (syncs all lectures)

2. **Verify deployment:**
   - Check that HTML files exist in `docs/slides/`
   - Check that `_files/` directories were copied (RevealJS assets)
   - Check that `docs/Figures/` was synced from `Figures/`

3. **Verify interactive charts** (if applicable):
   - Check rendered HTML for interactive widget elements
   - Confirm charts load without errors

4. **Verify TikZ SVGs** (if applicable):
   - Check that all referenced SVG files exist in `docs/Figures/LectureN/`
   - Test that SVGs render correctly in the browser

5. **Open in browser** for visual verification:
   ```bash
   open docs/slides/LectureX_Name.html
   ```
   - Confirm slides render, images display, navigation works
   - Test on mobile viewport if applicable

6. **Commit and push** the `docs/` directory:
   ```bash
   git add docs/
   git commit -m "Deploy LectureN slides to GitHub Pages"
   git push
   ```

7. **Report results** — confirm GitHub Pages URL is accessible.

---

## What the Sync Script Does

- Renders all `.qmd` files in `Quarto/` (skips `*_backup*` files)
- Copies HTML and `_files/` directories to `docs/slides/`
- Copies Beamer PDFs from `Slides/` to `docs/slides/`
- Syncs `Figures/` to `docs/Figures/` using rsync

---

## Manual Quarto Render (if sync script unavailable)

```bash
# Render a single lecture
cd Quarto
quarto render Lecture4_Topic.qmd

# Copy to docs
mkdir -p ../docs/slides
cp Lecture4_Topic.html ../docs/slides/
cp -r Lecture4_Topic_files/ ../docs/slides/Lecture4_Topic_files/
```

---

## Troubleshooting

| Issue | Likely Cause | Fix |
|-------|-------------|-----|
| SVGs not loading | Wrong path in QMD | Check relative path from `docs/slides/` |
| Charts not interactive | plotly not bundled | Check `self-contained: true` in YAML |
| 404 on GitHub Pages | Not pushed or Pages not configured | Push and check Settings > Pages |
