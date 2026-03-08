---
mode: 'agent'
description: 'Validate bibliography entries against citations in all lecture files. Find missing entries, unused references, and citation key typos.'
---

# Validate Bibliography

Cross-reference all citations in lecture files against bibliography entries.

## Steps

1. **Read the bibliography file** (`Bibliography_base.bib`) and extract all citation keys.

2. **Scan all lecture files for citation keys:**
   - `.tex` files: look for `\cite{`, `\citet{`, `\citep{`, `\citeauthor{`, `\citeyear{`
   - `.qmd` files: look for `@key`, `[@key]`, `[@key1; @key2]`
   - Extract all unique citation keys used

3. **Cross-reference:**
   - **Missing entries:** Citations used in lectures but NOT in bibliography → CRITICAL
   - **Unused entries:** Entries in bibliography not cited anywhere → informational
   - **Potential typos:** Similar-but-not-matching keys (e.g., `smith2020` vs `Smith2020`)

4. **Check entry quality** for each bib entry:
   - Required fields present (author, title, year, journal/booktitle)
   - Author field properly formatted (`Surname, First` or `First Surname`)
   - Year is reasonable (no future years, no dates formatted as text)
   - No malformed characters or encoding issues

5. **Report findings:**

```markdown
## Bibliography Validation Report

**Date:** [YYYY-MM-DD]

### Missing Entries (CRITICAL — Fix Before Compiling)
| Citation Key | Used In | Status |
|-------------|---------|--------|
| smith2020 | Lecture3.tex | Missing from bib |

### Potential Typos
| Key Used | Similar Key in Bib | Suggested Fix |
|----------|--------------------|---------------|
| Smith2020 | smith2020 | Use lowercase |

### Unused Entries (Informational)
[List of keys in bib but not cited]

### Quality Issues
| Entry | Issue | Fix |
|-------|-------|-----|
| jones1985 | Missing journal field | Add journal name |

### Summary
- Total citations used: N
- Missing from bib: N (CRITICAL)
- Typos detected: N
- Unused entries: N
- Quality issues: N
```

---

## Files to Scan

```
Slides/*.tex
Quarto/*.qmd
```

## Bibliography Location

```
Bibliography_base.bib  (repo root)
```

---

## Notes

- Missing entries will cause LaTeX compilation to fail with `undefined citation` warnings
- Run this skill before every compilation to avoid surprises
- Add missing entries to `Bibliography_base.bib`, not to local `.bib` files
