---
mode: 'agent'
description: 'Perform adversarial visual audit of Quarto or Beamer slides. Checks for overflow, font consistency, box fatigue, spacing, and layout issues.'
---

# Visual Audit of Slide Deck

Perform a thorough visual layout audit of a slide deck. Produces a report **without editing any files**.

## Steps

1. **Read the slide file** from the given path

2. **For Quarto (.qmd) files:**
   - Note: rendering requires `quarto render Quarto/FILENAME.qmd`
   - Inspect the source for common issues

3. **For Beamer (.tex) files:**
   - Compile and check for overfull hbox warnings

4. **Audit every slide for:**

### OVERFLOW
- Content exceeding slide boundaries
- Overfull hbox (LaTeX) — any value > 10pt is a problem
- Text running off screen (Quarto)

### FONT CONSISTENCY
- Inline font-size overrides (e.g., `\tiny`, `\scriptsize` in Beamer)
- Inconsistent font sizes across similar slide types
- Font reduction below 0.85em / `\footnotesize`

### BOX FATIGUE
- More than 2 colored boxes on one slide
- Wrong box type for the content (e.g., using `highlightbox` for a definition)

### SPACING
- Missing negative margins before/after figures
- Missing `fig-align: center` in Quarto
- Excessive whitespace causing text to float

### LAYOUT
- Missing transition slides between major sections
- Missing framing sentences (topic sentence at start, punchline at end)
- Semantic colors used inconsistently (e.g., blue for student, red for firm)

5. **Apply the spacing-first principle** for overflow fixes:
   1. Reduce vertical spacing with negative margins (`\vspace{-0.3cm}`)
   2. Consolidate bullet lists
   3. Move displayed equations inline
   4. Reduce image/SVG size
   5. Last resort: font size reduction (never below `\footnotesize`)

6. **Produce a report** organized by slide with severity and specific recommendations:
   - **Critical:** Content is cut off or illegible
   - **High:** Significant layout problem affecting readability
   - **Medium:** Style inconsistency
   - **Low:** Minor cleanup

7. **Save the report** to `quality_reports/[FILENAME]_visual_audit.md`
