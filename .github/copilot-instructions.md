# GitHub Copilot Global Instructions

<!-- Academic Economics Workflow — Copilot Edition -->
<!-- Adapted from Zsijiang/claude-code-my-workflow -->

## Core Principles

- **Plan first** — for any non-trivial task, outline the approach before writing code or text
- **Verify after** — compile/render and confirm output at the end of every task
- **Single source of truth** — Beamer `.tex` is authoritative; Quarto `.qmd` derives from it
- **Quality gates** — nothing ships below 80/100
- **Economics focus** — apply rigorous economic thinking: identification, mechanisms, policy implications

---

## Folder Structure Convention

```
project/
├── .github/                     # Copilot instructions and prompt skills
├── Bibliography_base.bib        # Centralized bibliography
├── Figures/                     # Figures and images
├── Preambles/header.tex         # LaTeX headers / Beamer theme
├── Slides/                      # Beamer .tex lecture files
├── Quarto/                      # RevealJS .qmd files + theme
├── docs/                        # GitHub Pages (auto-generated)
├── scripts/R/                   # R analysis scripts
├── output/                      # Figures, tables, RDS files
├── quality_reports/             # Plans, session logs, merge reports
├── master_supporting_docs/      # Papers and existing slides
└── templates/                   # Session log, quality report templates
```

---

## LaTeX / Beamer Commands

```bash
# 3-pass XeLaTeX compilation (always use XeLaTeX, never pdflatex)
cd Slides
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode FILENAME.tex
BIBINPUTS=..:$BIBINPUTS bibtex FILENAME
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode FILENAME.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode FILENAME.tex

# Deploy Quarto to GitHub Pages
./scripts/sync_to_docs.sh LectureN
```

---

## R Code Conventions

- Use `tidyverse` for data manipulation
- Use `fixest` for panel regression (faster than `lfe`, supports DiD)
- Use `modelsummary` for publication-ready tables
- Use `ggplot2` for all figures; set `bg = "transparent"` for Beamer compatibility
- Always `set.seed(42)` at the top
- Save all objects with `saveRDS()`; save figures with explicit `ggsave()` dimensions
- Use relative paths from the project root

---

## Quality Thresholds

| Score | Gate     | Meaning                      |
|-------|----------|------------------------------|
| 80    | Commit   | Good enough to save          |
| 90    | PR       | Ready for deployment         |
| 95    | Excellence | Aspirational               |

---

## Economics Writing Standards

- Motivation before formalism — always explain the economic intuition first
- State identification assumptions explicitly
- Report effect sizes, not just statistical significance
- Cluster standard errors at the appropriate level and justify the choice
- Distinguish descriptive, correlational, and causal claims
- Cite seminal and recent work; do not fabricate citations

---

## Prompt Skills Quick Reference

| Skill File | What It Does |
|------------|-------------|
| `compile-latex` | 3-pass XeLaTeX + bibtex compilation |
| `deploy` | Render Quarto + sync to docs/ |
| `extract-tikz` | TikZ → PDF → SVG pipeline |
| `create-tikz-diagram` | Draw economics diagrams with TikZ |
| `create-economics-figure` | Supply/demand, game theory, macro diagrams |
| `data-visualization` | Publication-ready R/ggplot2 figures |
| `proofread` | Grammar/typo/overflow/consistency review |
| `write-academic-paper` | Full economics paper writing workflow |
| `visual-audit` | Slide layout audit |
| `pedagogy-review` | Narrative, notation, pacing review |
| `review-r` | R code quality review |
| `qa-quarto` | Adversarial Quarto vs Beamer QA |
| `slide-excellence` | Combined multi-agent review |
| `translate-to-quarto` | Beamer → Quarto translation |
| `validate-bib` | Cross-reference citations |
| `devils-advocate` | Challenge slide design |
| `create-lecture` | Full lecture creation |
| `commit` | Stage, commit, PR, merge |
| `lit-review` | Literature search + synthesis |
| `research-ideation` | Research questions + strategies |
| `interview-me` | Interactive research interview |
| `review-paper` | Manuscript review |
| `data-analysis` | End-to-end R analysis |
