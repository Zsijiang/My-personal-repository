---
mode: 'agent'
description: 'Multi-agent slide review running visual audit, pedagogical review, and proofreading in sequence. Use for comprehensive quality check before milestones.'
---

# Slide Excellence Review

Run a comprehensive multi-dimensional review of lecture slides. Multiple review passes analyze the file independently, then results are synthesized.

## Steps

### Step 1: Identify the File

Parse the given filename. Resolve path in `Quarto/` or `Slides/`.

### Step 2: Run Review Passes

**Pass 1: Visual Audit**
Follow the `visual-audit` skill:
- Overflow, font consistency, box fatigue, spacing, images
- Save: `quality_reports/[FILE]_visual_audit.md`

**Pass 2: Pedagogical Review**
Follow the `pedagogy-review` skill:
- 13 pedagogical patterns, narrative, pacing, notation
- Save: `quality_reports/[FILE]_pedagogy_report.md`

**Pass 3: Proofreading**
Follow the `proofread` skill:
- Grammar, typos, consistency, academic quality, citations
- Save: `quality_reports/[FILE]_report.md`

**Pass 4: Economics Content Review** (for economics lectures)
- Are all identification assumptions stated?
- Are effect sizes reported with economic interpretation?
- Is causal language used only where justified?
- Are all citations present and accurate?
- Save: `quality_reports/[FILE]_content_review.md`

### Step 3: Synthesize Combined Summary

```markdown
# Slide Excellence Review: [Filename]

## Overall Quality Score: [EXCELLENT / GOOD / NEEDS WORK / POOR]

| Dimension | Critical | Medium | Low |
|-----------|----------|--------|-----|
| Visual/Layout | | | |
| Pedagogical | | | |
| Proofreading | | | |
| Economics Content | | | |

### Critical Issues (Immediate Action Required)
[List each issue with slide reference and fix suggestion]

### Medium Issues (Next Revision)
[List]

### Recommended Next Steps
1. [Most impactful action]
2. [Second most impactful]
3. [Third]
```

---

## Quality Score Rubric

| Score | Critical Issues | Medium Issues | Meaning |
|-------|-----------------|---------------|---------|
| Excellent | 0–2 | 0–5 | Ready to present |
| Good | 3–5 | 6–15 | Minor refinements needed |
| Needs Work | 6–10 | 16–30 | Significant revision required |
| Poor | 11+ | 31+ | Major restructuring needed |

---

## Notes

- This skill runs the other review skills in sequence
- For a quick check, run `visual-audit` or `proofread` individually
- Save all reports before presenting the synthesis to the user
