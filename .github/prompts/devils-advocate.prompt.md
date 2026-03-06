---
mode: 'agent'
description: 'Challenge slide design with 5–7 pedagogical questions. Checks concept ordering, prerequisites, cognitive load, and alternative presentations. Use before finalizing a lecture.'
---

# Devil's Advocate Review

Critically examine a slide deck and challenge its design with 5–7 specific pedagogical questions.

**Philosophy:** "We arrive at the best possible presentation through active dialogue."

---

## Setup

1. **Read the target lecture file**
2. **Note the course context:** What lecture is this? What came before? What comes after?
3. **Read from a student's perspective:** What do they know entering this lecture?

---

## Challenge Categories

Generate 5–7 challenges from these categories:

### 1. Ordering Challenges
> "Could students understand this better if we showed X before Y?"

Example: "You introduce the formal model before any empirical motivation. Should the empirical fact come first?"

### 2. Prerequisite Challenges
> "Do students have the background for this notation at this point?"

Example: "Slide 8 uses the GMM framework, but this is introduced in Lecture 6. If this is Lecture 4, students won't have seen it."

### 3. Gap Challenges
> "Should we include an intuitive example before this formal proof?"

Example: "The proof of Theorem 2 has no worked example. Students need to see the math in action."

### 4. Alternative Presentation Challenges
> "Here are 2 other ways to visualize/present this concept."

Example: "The production function slide uses a 3D equation. A 2D isoquant diagram might be more intuitive."

### 5. Notation Conflict Challenges
> "This symbol conflicts with earlier lecture usage."

Example: "You use $\sigma$ for standard deviation here, but in Lecture 2 it was used for the substitution elasticity."

### 6. Cognitive Load Challenges
> "This slide has too many new symbols. Can we split?"

Example: "Slide 12 introduces 4 new variables simultaneously. Consider breaking into 2 slides."

### 7. Economic Interpretation Challenges
> "The math is correct, but what is the economic intuition?"

Example: "Theorem 3 states a convergence result but doesn't explain what it means for policy or for firm behavior."

---

## Output Format

```markdown
# Devil's Advocate: [Lecture Title]

## Challenges

### Challenge 1: [Category] — [Short title]
**Question:** [The specific pedagogical question]
**Why it matters:** [What could go wrong if unaddressed]
**Suggested resolution:** [Specific, actionable change]
**Slides affected:** [Numbers or titles]
**Severity:** High / Medium / Low

[Repeat for 5–7 challenges]

## Summary Verdict

**Strengths:** [2–3 things the deck does well]
**Critical changes (before teaching):** [0–2 must-fix items]
**Suggested improvements (nice-to-have):** [2–3 items]
```

---

## Principles

- **Be specific:** Reference exact slides and notation
- **Be constructive:** Every challenge has a suggested resolution
- **Be honest:** If the deck is good, say so
- **Prioritize:** Notation conflicts > ordering > gaps > alternatives
- **Think like a student:** Where do they get lost?
