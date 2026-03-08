---
mode: 'agent'
description: 'Adversarial Quarto vs Beamer QA. Find issues in the Quarto translation compared to the Beamer benchmark and fix them iteratively.'
---

# Adversarial Quarto vs Beamer QA

Compare Quarto HTML slides against their Beamer PDF benchmark using an iterative find-and-fix loop.

**Philosophy:** The Beamer PDF is the gold standard. The Quarto translation must be at least as good in every dimension.

---

## Hard Gates (Non-Negotiable)

| Gate | Condition |
|------|-----------|
| **Overflow** | NO content cut off |
| **Plot Quality** | Interactive charts ≥ static plots |
| **Content Parity** | No missing slides/equations/text |
| **Visual Regression** | Quarto ≥ Beamer in all dimensions |
| **Slide Centering** | Content centered, no jumping |
| **Notation Fidelity** | All math verbatim from Beamer |

---

## Workflow

```
Pre-flight → Audit (find issues) → Fix → Re-Audit → Loop until APPROVED (max 5 rounds)
```

### Phase 0: Pre-flight

1. Locate Beamer (.tex) and Quarto (.qmd/.html) files
2. Re-render Quarto if QMD is newer than HTML:
   ```bash
   cd Quarto && quarto render FILENAME.qmd
   ```
3. Verify TikZ SVGs exist in `Figures/LectureN/`

### Phase 1: Initial Audit

Systematically compare Beamer and Quarto, slide by slide:

**Check for each slide:**
- [ ] Same content (no omissions)
- [ ] Math notation identical
- [ ] Figures present and correct
- [ ] Colored boxes / callouts equivalent
- [ ] No overflow or cut-off content
- [ ] Slide title matches frame title

**Report format:**
```markdown
## Audit Round [N]: [Lecture]

### Hard Gate Status
| Gate | Status |
|------|--------|
| Overflow | ✅/❌ |
| Content Parity | ✅/❌ |
| Notation Fidelity | ✅/❌ |

### Issues Found
| Slide | Severity | Issue | Fix |
|-------|----------|-------|-----|
| 3 | Critical | Math missing: $\hat{\beta}$ | Add equation |
| 7 | High | TikZ SVG not loading | Fix path |
```

### Phase 2: Fix Issues

For each issue found (Critical → High → Medium → Low):

1. Apply fix to the `.qmd` file
2. Re-render: `quarto render FILENAME.qmd`
3. Verify the fix resolved the issue

### Phase 3: Re-Audit

Repeat Phase 1 on the updated slides. If all hard gates pass → **APPROVED**.

If issues remain after 5 rounds, stop and report to user with a list of outstanding issues.

---

## Final Report

Save to `quality_reports/[Lecture]_qa_final.md`:

```markdown
# QA Final Report: [Lecture]

**Outcome:** APPROVED / NEEDS MANUAL REVIEW
**Rounds:** [N]

## Hard Gate Status (Final)
[All gates with ✅/❌]

## Remaining Issues (if any)
[List of issues that could not be automatically resolved]
```
