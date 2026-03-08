---
mode: 'agent'
description: 'Run the proofreading protocol on lecture files. Checks grammar, typos, overflow, consistency, and academic writing quality. Produces a report without editing files.'
---

# Proofread Lecture Files

Run the mandatory proofreading protocol on lecture files. This produces a report of all issues found **WITHOUT editing any source files**.

## Steps

1. **Identify files to review:**
   - If a specific filename is given: review that file only
   - If "all" is given: review all lecture files in `Slides/` and `Quarto/`

2. **For each file, check for:**

   **GRAMMAR:** Subject-verb agreement, articles (a/an/the), prepositions, tense consistency

   **TYPOS:** Misspellings, search-and-replace artifacts, duplicated words

   **OVERFLOW:** Overfull hbox (LaTeX), content exceeding slide boundaries (Quarto)

   **CONSISTENCY:** Citation format, notation, terminology

   **ACADEMIC QUALITY:** Informal language, missing words, awkward constructions, passive-voice overuse

3. **Produce a detailed report** for each file listing every finding with:
   - Location (line number or slide title)
   - Current text (what's wrong)
   - Proposed fix (what it should be)
   - Category and severity (Critical / High / Medium / Low)

4. **Save each report** to `quality_reports/`:
   - For `.tex` files: `quality_reports/FILENAME_report.md`
   - For `.qmd` files: `quality_reports/FILENAME_qmd_report.md`

5. **IMPORTANT: Do NOT edit any source files.**
   Only produce the report. Fixes are applied separately after user review.

6. **Present summary** to the user:
   - Total issues found per file
   - Breakdown by category
   - Most critical issues highlighted

## Economics-Specific Checks

- Are identification assumptions stated explicitly?
- Is causal language used only when causality is established?
- Are effect sizes reported alongside significance?
- Is notation consistent with standard economics conventions?
- Are policy implications clearly connected to findings?
