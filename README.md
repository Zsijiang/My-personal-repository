# My Personal Repository — GitHub Copilot Skills for Academic Economics

A collection of GitHub Copilot prompt skills for academic economics work: lecture creation, paper writing, data analysis, visualization, and more. Adapted from [Zsijiang/claude-code-my-workflow](https://github.com/Zsijiang/claude-code-my-workflow).

---

## Quick Start

### Scenario 1: Using in VS Code (Recommended)

1. Open the repository in VS Code with the GitHub Copilot extension installed.
2. Open Copilot Chat (`Ctrl+Shift+I` / `Cmd+Shift+I`).
3. Use `/` to browse available prompt skills, or type `@workspace /skill-name`.
4. Select a prompt from `.github/prompts/` to run it.

### Scenario 2: Using with GitHub Copilot in the Browser

1. Navigate to any file in this repository on GitHub.
2. Open Copilot Chat.
3. Reference a prompt file: "Use the instructions in `.github/prompts/data-analysis.prompt.md` to..."

### Scenario 3: Using Prompt Files Directly

Copy the content of any `.github/prompts/*.prompt.md` file and paste it into any AI assistant (Copilot, ChatGPT, Claude, etc.) as a system prompt or instruction.

---

## Available Skills

### ✍️ Writing Skills

| Skill | File | What It Does |
|-------|------|-------------|
| **Proofread** | `proofread.prompt.md` | Grammar, typos, overflow, consistency check. Produces a report without editing files. |
| **Write Academic Paper** | `write-academic-paper.prompt.md` | Full economics paper workflow: outline → intro → core sections → polish. |
| **Review Paper** | `review-paper.prompt.md` | Comprehensive manuscript review covering argument, econometrics, literature, referee objections. |
| **Literature Review** | `lit-review.prompt.md` | Structured literature search and synthesis with BibTeX extraction and gap identification. |

### 🎨 Drawing & Visualization Skills

| Skill | File | What It Does |
|-------|------|-------------|
| **Create TikZ Diagram** | `create-tikz-diagram.prompt.md` | Draw economics diagrams: supply/demand, indifference curves, game theory, IS-LM, DAGs. |
| **Extract TikZ** | `extract-tikz.prompt.md` | Extract TikZ diagrams from Beamer, compile to PDF, convert to SVG for Quarto. |
| **Create Economics Figure** | `create-economics-figure.prompt.md` | Publication-ready economics figures: coefficient plots, event studies, binscatters, maps. |
| **Data Visualization** | `data-visualization.prompt.md` | All standard chart types with R/ggplot2: bar, line, scatter, density, heatmap. |

### 💻 Code Writing Skills

| Skill | File | What It Does |
|-------|------|-------------|
| **Data Analysis** | `data-analysis.prompt.md` | End-to-end R analysis: load → EDA → regression → publication-ready tables and figures. |
| **Review R** | `review-r.prompt.md` | R code quality review: reproducibility, statistical correctness, style. |
| **Compile LaTeX** | `compile-latex.prompt.md` | 3-pass XeLaTeX + bibtex compilation for Beamer lecture slides. |

### 📊 Economics Research Skills

| Skill | File | What It Does |
|-------|------|-------------|
| **Research Ideation** | `research-ideation.prompt.md` | Generate research questions, hypotheses, and identification strategies. |
| **Interview Me** | `interview-me.prompt.md` | Interactive interview to formalize a research idea into a specification document. |
| **Validate Bibliography** | `validate-bib.prompt.md` | Cross-reference citations against bibliography; find missing entries and typos. |

### 🎓 Lecture & Slides Skills

| Skill | File | What It Does |
|-------|------|-------------|
| **Create Lecture** | `create-lecture.prompt.md` | Full economics lecture creation with pedagogy standards and Beamer patterns. |
| **Visual Audit** | `visual-audit.prompt.md` | Slide layout audit: overflow, font consistency, box fatigue, spacing. |
| **Pedagogy Review** | `pedagogy-review.prompt.md` | 13-pattern pedagogical review: narrative arc, notation density, worked examples. |
| **Slide Excellence** | `slide-excellence.prompt.md` | Multi-pass combined review (visual + pedagogy + proofreading + economics content). |
| **Translate to Quarto** | `translate-to-quarto.prompt.md` | Full Beamer → Quarto RevealJS translation with TikZ SVG and QA. |
| **QA Quarto** | `qa-quarto.prompt.md` | Adversarial Quarto vs Beamer comparison with iterative fix loop. |
| **Devil's Advocate** | `devils-advocate.prompt.md` | Challenge slide design: ordering, prerequisites, cognitive load, alternatives. |

### 🔧 Workflow Skills

| Skill | File | What It Does |
|-------|------|-------------|
| **Deploy** | `deploy.prompt.md` | Render Quarto slides and sync to docs/ for GitHub Pages deployment. |
| **Commit** | `commit.prompt.md` | Stage, commit, create PR, and merge to main. |

---

## Repository Structure

```
.github/
├── copilot-instructions.md      # Global Copilot instructions
└── prompts/                     # All skill prompt files
    ├── compile-latex.prompt.md
    ├── commit.prompt.md
    ├── create-economics-figure.prompt.md
    ├── create-lecture.prompt.md
    ├── create-tikz-diagram.prompt.md
    ├── data-analysis.prompt.md
    ├── data-visualization.prompt.md
    ├── deploy.prompt.md
    ├── devils-advocate.prompt.md
    ├── extract-tikz.prompt.md
    ├── interview-me.prompt.md
    ├── lit-review.prompt.md
    ├── pedagogy-review.prompt.md
    ├── proofread.prompt.md
    ├── qa-quarto.prompt.md
    ├── research-ideation.prompt.md
    ├── review-paper.prompt.md
    ├── review-r.prompt.md
    ├── slide-excellence.prompt.md
    ├── translate-to-quarto.prompt.md
    ├── validate-bib.prompt.md
    ├── visual-audit.prompt.md
    └── write-academic-paper.prompt.md
README.md
```

---

## Economics Focus

All skills are tailored for **economics research and teaching**:

- **Identification-first thinking:** Always ask about causal identification
- **Effect size reporting:** Pair statistical significance with economic magnitude
- **Standard tools:** R (`fixest`, `modelsummary`, `ggplot2`), LaTeX/Beamer, Quarto
- **Publication standards:** Top-5 journal quality for papers; rigorous pedagogy for lectures
- **Diagram conventions:** TikZ for supply/demand, game theory, macroeconomic models

---

## Prerequisites

| Tool | Required For |
|------|-------------|
| VS Code + GitHub Copilot | Running prompt skills in VS Code |
| XeLaTeX (TeX Live / MacTeX) | LaTeX compilation skills |
| Quarto | Web slide deployment |
| R + tidyverse + fixest | Data analysis skills |
| pdf2svg | TikZ extraction |
| gh CLI | Git workflow skills |

Not all tools are needed — install only what your project uses.

---

## Credits

Adapted from [Zsijiang/claude-code-my-workflow](https://github.com/Zsijiang/claude-code-my-workflow), which was extracted from **Econ 730: Causal Panel Data** at Emory University.
