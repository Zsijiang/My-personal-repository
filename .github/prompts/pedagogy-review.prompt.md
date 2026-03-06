---
mode: 'agent'
description: 'Run holistic pedagogical review on lecture slides. Checks narrative arc, student prerequisites, worked examples, notation clarity, and deck pacing.'
---

# Pedagogical Review of Lecture Slides

Perform a comprehensive pedagogical review of an economics lecture deck.

## Pedagogical Patterns (13 Checks)

### Pattern 1: Motivation First
Every new concept must be preceded by economic motivation (a puzzle, a fact, a policy question).
- ❌ "Let $X$ denote a random variable..."
- ✅ "Why do firms invest more during booms? Consider a simple model..."

### Pattern 2: Formal → Intuition Pairing
Every formal statement (theorem, lemma, definition) must be paired with an intuitive explanation.

### Pattern 3: Worked Example Proximity
A worked example must appear within 2 slides of every new definition or theorem.

### Pattern 4: Notation Density
No more than 3 new symbols per slide. Exceeding this creates cognitive overload.

### Pattern 5: Prerequisite Clarity
If a concept requires prior knowledge, it must be stated explicitly ("Recall from Lecture 3...").

### Pattern 6: Empirical Thread
At least one running real-world application must be threaded throughout the lecture.

### Pattern 7: Transition Slides
Major conceptual pivots (between sections) need transition slides that restate where we've been and where we're going.

### Pattern 8: Box Usage
Colored boxes (keybox, highlightbox, definitionbox) used at most 2 per slide, and for their intended purpose.

### Pattern 9: Socratic Questions
2–3 rhetorical questions embedded to prompt student thinking ("What happens if we relax this assumption?").

### Pattern 10: Economic Significance
Results presented with economic interpretation, not just mathematical statements.

### Pattern 11: Notation Consistency
All symbols consistent with previous lectures in the course.

### Pattern 12: Figure-Slide Linking
Every figure on a slide has a 1–2 sentence interpretation immediately adjacent.

### Pattern 13: Conclusion
Lecture ends with a summary of key takeaways and a bridge to the next lecture.

---

## Deck-Level Analysis

- **Narrative arc:** Does the lecture tell a coherent story from motivation to conclusion?
- **Pacing:** Are there too many dense slides in a row? Is there breathing room?
- **Visual rhythm:** Is there variety between text slides, diagram slides, and example slides?
- **Student perspective:** Where will students get confused? What questions will they ask?

---

## Output Format

```markdown
# Pedagogical Review: [Lecture Title]

**Patterns followed:** X/13
**Patterns violated:** [List]

## Critical Issues

1. [Pattern N violated] — [Specific slide] — [Recommendation]
2. ...

## Deck-Level Assessment

- **Narrative arc:** [Rating + comments]
- **Pacing:** [Rating + comments]
- **Visual rhythm:** [Rating + comments]
- **Notation density:** [Rating + comments]

## Recommendations (Priority Ordered)

1. [Most important fix]
2. [Second most important]
3. [Third]
```

**Save to:** `quality_reports/[FILENAME]_pedagogy_report.md`

---

## Notes

- This is a **read-only review** — no files are edited
- For visual layout issues, use the `visual-audit` skill instead
- For a combined review, use the `slide-excellence` skill
