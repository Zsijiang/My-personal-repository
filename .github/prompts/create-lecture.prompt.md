---
mode: 'agent'
description: 'Create new Beamer lecture from papers and materials. Guided workflow with notation consistency and economics pedagogy standards.'
---

# Lecture Creation Workflow

Create a beautiful, pedagogically excellent Beamer lecture deck on an economics topic.

**This is a collaborative, iterative process. The instructor drives the vision; Copilot is a thinking partner.**

---

## Constraints (Non-Negotiable)

1. **Motivation before formalism** — no exceptions: intuition → example → formal statement
2. Every new symbol MUST be consistent with previous lectures' notation
3. Worked example within 2 slides of every definition
4. Max 2 colored boxes per slide
5. No `\pause` or overlay commands (they break Quarto translation)
6. Transition slides at major conceptual pivots
7. Thread at least 1 running empirical application throughout
8. All citations verified against `Bibliography_base.bib`
9. **Work in batches of 5–10 slides** — share for feedback before continuing

---

## Workflow

### Phase 0: Intake & Context
- Read any provided papers, slides, code
- Review previous lecture's structure and ending
- State pedagogical goal, confirm with user

### Phase 1: Paper Analysis (When Papers Provided)
- Extract key ideas and slide-worthy content
- Map paper notation → course notation
- Present summary for approval

### Phase 2: Structure Proposal
- Propose outline (5-Act or 3-Part template)
- List TikZ diagrams and R figures needed
- List new notation to introduce
- **GATE: User approves before writing slides**

### Phase 3: Draft Slides (Iterative)
Work in batches of 5–10 slides. Apply these patterns:

#### Slide Types
| Type | Content |
|------|---------|
| **Motivation** | Why this matters (empirical fact, puzzle, policy question) |
| **Definition** | Formal statement + economic interpretation |
| **Worked Example** | Concrete numerical or graphical example |
| **Proposition/Theorem** | Formal result + proof sketch |
| **Intuition** | Non-technical explanation of the result |
| **Application** | Connection to data, policy, or real-world case |
| **Transition** | Section bridge with overview of upcoming content |

#### Quality Checks Per Batch
- [ ] Every definition has motivation + worked example within 2 slides
- [ ] Max 2 colored boxes per slide
- [ ] No `\pause` or overlay commands
- [ ] Consistent notation with previous lectures
- [ ] Citations properly formatted (`\citet{}`, `\citep{}`)

### Phase 4: Figures & Code
- R scripts following conventions in `scripts/R/`
- TikZ diagrams inline in Beamer source (single source of truth)
- Save RDS objects for future Quarto integration

### Phase 5: Polish & Compile
- Full 3-pass compilation
- Run proofreading check
- Run visual audit

---

## Beamer Code Patterns

### Basic Slide
```latex
\begin{frame}{Slide Title}

\textbf{Economic motivation:} [1–2 sentences explaining why this matters]

\medskip

\begin{keybox}
  \textbf{Definition:} [Formal statement]
\end{keybox}

\medskip

\textbf{Intuition:} [Non-technical explanation]

\end{frame}
```

### Theorem Slide
```latex
\begin{frame}{Theorem: [Name]}

\begin{theorem}[Author, Year]
  Under Assumptions 1–3, the estimator $\hat{\beta}$ satisfies...
\end{theorem}

\medskip

\textbf{Key implication:} [One sentence on what this means economically]

\textbf{Proof sketch:} [2–3 bullet points on the main steps]

\end{frame}
```

### Two-Column Slide (Diagram + Text)
```latex
\begin{frame}{[Title]}

\begin{columns}
  \begin{column}{0.5\textwidth}
    \begin{tikzpicture}
      % diagram here
    \end{tikzpicture}
  \end{column}
  \begin{column}{0.5\textwidth}
    \begin{itemize}
      \item [Point 1]
      \item [Point 2]
      \item [Point 3]
    \end{itemize}
  \end{column}
\end{columns}

\end{frame}
```

---

## Post-Creation Checklist

```
[ ] Lecture compiles without errors
[ ] No overfull hbox > 10pt
[ ] All citations resolve
[ ] Every definition has motivation + worked example
[ ] Max 2 colored boxes per slide
[ ] 2–3 Socratic questions embedded
[ ] Transition slides between sections
[ ] At least 1 running application threaded throughout
[ ] Proofreading complete
```
