---
mode: 'agent'
description: 'Run the R code review protocol on R scripts. Checks code quality, reproducibility, domain correctness, and professional standards. Produces a report without editing files.'
---

# Review R Code

Run the comprehensive R code review protocol. Produces a report **without editing any files**.

## Steps

1. **Identify scripts to review:**
   - Specific `.R` filename → review that file only
   - `LectureN` → review all R scripts for that lecture
   - `all` → review all scripts in `scripts/R/`

2. **For each script, evaluate:**

### Code Quality
- [ ] Packages loaded with `library()` at the top (never `require()`)
- [ ] `set.seed()` present if any randomness
- [ ] No `setwd()` (use relative paths)
- [ ] No `rm(list = ls())` (use script isolation instead)
- [ ] All functions have meaningful names (verb_noun pattern)
- [ ] No magic numbers — use named constants

### Reproducibility
- [ ] Script runs from top to bottom without errors
- [ ] All input files exist at stated paths
- [ ] `saveRDS()` called for all computed objects
- [ ] Output directories created with `dir.create(..., recursive = TRUE)`
- [ ] Session info saved: `writeLines(capture.output(sessionInfo()), "output/session_info.txt")`

### Statistical Correctness
- [ ] Appropriate standard errors (clustered, robust, or default — and justified)
- [ ] No p-hacking indicators (no specification search without pre-registration)
- [ ] Effect sizes reported alongside p-values
- [ ] Sample restrictions documented and justified
- [ ] Multicollinearity checked for regression models

### R/Econometrics-Specific
- [ ] `fixest` used for panel models (not `lfe` or `felm`)
- [ ] `modelsummary` used for tables (preferred over `stargazer`)
- [ ] `ggplot2` used for all figures
- [ ] `bg = "transparent"` in all `ggsave()` calls for Beamer compatibility
- [ ] Axis labels in sentence case with units
- [ ] Figure dimensions explicitly set in `ggsave()`

### Performance
- [ ] No redundant data copies (use pipes, not intermediate objects when possible)
- [ ] Large joins checked for cartesian products
- [ ] `complete.cases()` or explicit `na.action` for regressions

3. **Produce a detailed report** saved to `quality_reports/[script_name]_r_review.md`:
   - Severity: Critical / High / Medium / Low
   - Location: line number
   - Issue description
   - Suggested fix

4. **Present summary:**
   - Total issues per script
   - Breakdown by severity
   - Top 3 most critical issues

## Severity Definitions

| Level | Meaning | Examples |
|-------|---------|---------|
| Critical | Breaks reproducibility or correctness | Wrong SE, path hardcoded, seed missing |
| High | Poor practice, likely causes issues | `require()`, no `saveRDS()`, no output dir |
| Medium | Style/readability issues | Magic numbers, poor variable names |
| Low | Minor cleanup | Unused imports, extra whitespace |
