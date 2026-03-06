---
mode: 'agent'
description: 'Translate Beamer LaTeX slides to Quarto RevealJS HTML. Full workflow with TikZ SVG extraction and quality assurance.'
---

# Beamer → Quarto Translation Workflow

Full translation of a Beamer LaTeX lecture to Quarto RevealJS HTML slides.

**CRITICAL: The Beamer `.tex` file is the SINGLE SOURCE OF TRUTH. All content edits go there first.**

---

## Phase 0: Pre-Flight Checks

### Environment Parity
Scan Beamer for all custom environments (keybox, highlightbox, definitionbox, etc.). Verify CSS equivalents exist in the Quarto theme SCSS. If any are missing, create them first.

### TikZ Freshness
Run the `extract-tikz` skill to ensure SVGs match the current Beamer source.

### RDS Inventory
List all RDS files needed for interactive charts.

### Citation Mapping
Extract all citations from Beamer, confirm bibliography keys match.

---

## Phase 1: Pre-Translation Preparation

- Read the complete Beamer source, count frames
- Inventory all figures: TikZ → SVG, R plots → plotly/ggplot, photos → copy
- Note custom environments and their CSS equivalents

---

## Phase 2: Create QMD File with YAML Header

```yaml
---
title: "[Lecture Title]"
subtitle: "[Course Name]"
author: "[Author]"
format:
  revealjs:
    theme: [default, custom.scss]
    slide-number: true
    chalkboard: false
    width: 1280
    height: 720
    logo: "../Figures/logo.png"
    footer: "[Footer text]"
bibliography: "../Bibliography_base.bib"
---
```

---

## Phase 3: Frame-by-Frame Translation

For each Beamer frame, produce the equivalent Quarto slide:

**Beamer:**
```latex
\begin{frame}{Supply and Demand}
\begin{itemize}
  \item Markets clear when $Q_s = Q_d$
  \item The equilibrium price $P^*$ satisfies this condition
\end{itemize}
\end{frame}
```

**Quarto:**
```markdown
## Supply and Demand

- Markets clear when $Q_s = Q_d$
- The equilibrium price $P^*$ satisfies this condition
```

**Translation rules:**
- `\begin{frame}{Title}` → `## Title`
- `\begin{itemize}` / `\item` → `- ` (markdown list)
- `\begin{enumerate}` / `\item` → `1. ` (numbered list)
- `\begin{keybox}` → `::: {.callout-note}` (or custom CSS class)
- `\begin{columns}` → `::: {.columns}` layout
- TikZ diagrams → SVG references with 0-based indexing
- `\citet{key}` → `@key`; `\citep{key}` → `[@key]`
- Math: `$...$` stays as-is; `\[...\]` → `$$...$$`

---

## Phase 4: TikZ Integration

Reference extracted SVGs (0-based index):

```markdown
![](../Figures/LectureN/tikz_exact_00.svg){width=70% fig-align="center"}
```

---

## Phase 5: R Figure Integration

Replace static R figures with interactive plotly where appropriate:

```r
#| echo: false
library(plotly)
fig <- readRDS("../output/rds/figure_name.rds")
ggplotly(fig)
```

---

## Phase 6: First Render & Check

```bash
cd Quarto
quarto render FILENAME.qmd
open FILENAME.html
```

Go through EVERY slide and verify:
- [ ] Correct number of slides (matches Beamer frame count)
- [ ] All math renders correctly
- [ ] All figures display
- [ ] No content cut off
- [ ] Transitions work

---

## Phase 7: Polish

- Apply semantic colors
- Add framing sentences (topic at start, punchline at end)
- Verify interactive charts
- Run `visual-audit` and `proofread`

---

## Phase 8: Beamer Source Sync

Apply any corrections discovered during translation back to the Beamer source file.
