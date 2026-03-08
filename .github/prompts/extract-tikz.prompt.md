---
mode: 'agent'
description: 'Extract TikZ diagrams from Beamer source, compile to PDF, and convert to SVG for use in Quarto RevealJS slides. Use when updating TikZ diagrams for Quarto slides.'
---

# Extract TikZ Diagrams to SVG

Extract TikZ diagrams from the Beamer source, compile to multi-page PDF, and convert each page to SVG for use in Quarto slides.

## Steps

### Step 0: Freshness Check (MANDATORY)

Before compiling, verify that `extract_tikz.tex` matches the current Beamer source.

1. Find the Beamer source: `ls Slides/LECTURENAME*.tex`
2. Extract all `\begin{tikzpicture}` blocks from Beamer
3. Compare with `Figures/LECTURENAME/extract_tikz.tex`
4. If ANY difference exists: update `extract_tikz.tex` from the Beamer source
5. If `extract_tikz.tex` doesn't exist: create it from scratch

### Step 1: Navigate to the lecture's Figures directory

```bash
cd Figures/LECTURENAME
```

### Step 2: Compile the extract_tikz.tex file

```bash
TEXINPUTS=../../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode extract_tikz.tex
```

### Step 3: Count the number of pages

```bash
pdfinfo extract_tikz.pdf | grep "Pages:"
```

### Step 4: Convert each page to SVG using 0-BASED INDEXING

**CRITICAL: PDF pages are 1-indexed, but output SVG files are 0-indexed!**

```bash
PAGES=$(pdfinfo extract_tikz.pdf | grep "Pages:" | awk '{print $2}')
for i in $(seq 1 $PAGES); do
  idx=$(printf "%02d" $((i-1)))
  pdf2svg extract_tikz.pdf tikz_exact_$idx.svg $i
done
```

### Step 5: Sync to docs/ for deployment

```bash
cd ../..
./scripts/sync_to_docs.sh LECTURENAME
```

### Step 6: Verify SVG files

- Confirm 2–3 SVG files contain valid SVG markup
- Confirm file sizes are reasonable (not 0 bytes)

### Step 7: Report results

List all generated SVG files with their sizes.

---

## Source of Truth Reminder

TikZ diagrams **MUST** be edited in the Beamer `.tex` file first, then copied verbatim to `extract_tikz.tex`. **Never edit `extract_tikz.tex` directly.**

---

## Referencing SVGs in Quarto

In your `.qmd` file, reference SVGs like this (0-based index):

```markdown
![](../Figures/Lecture2/tikz_exact_00.svg){width=70%}
![](../Figures/Lecture2/tikz_exact_01.svg){width=70%}
```
