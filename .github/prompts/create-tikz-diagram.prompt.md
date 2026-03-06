---
mode: 'agent'
description: 'Create TikZ diagrams for economics: supply and demand, game theory payoff matrices, production functions, indifference curves, IS-LM, and other economic diagrams.'
---

# Create Economics TikZ Diagram

Draw publication-quality economics diagrams using TikZ/PGFPlots for use in Beamer slides or LaTeX papers.

## Common Economics Diagrams

### 1. Supply and Demand
```latex
\begin{tikzpicture}
  \begin{axis}[
    xlabel={Quantity}, ylabel={Price},
    xmin=0, xmax=10, ymin=0, ymax=10,
    axis lines=left,
    width=7cm, height=7cm,
  ]
    % Supply curve
    \addplot[thick, blue, domain=0:9] {x + 1} node[right] {$S$};
    % Demand curve
    \addplot[thick, red, domain=0:9] {10 - x} node[right] {$D$};
    % Equilibrium
    \addplot[dashed, gray] coordinates {(4.5,0) (4.5,5.5)};
    \addplot[dashed, gray] coordinates {(0,5.5) (4.5,5.5)};
    \node[fill=black, circle, inner sep=2pt] at (axis cs:4.5,5.5) {};
    \node[above right] at (axis cs:4.5,5.5) {$E^*$};
  \end{axis}
\end{tikzpicture}
```

### 2. Indifference Curves with Budget Constraint
```latex
\begin{tikzpicture}
  \begin{axis}[
    xlabel={Good 1}, ylabel={Good 2},
    xmin=0, xmax=6, ymin=0, ymax=6,
    axis lines=left,
    width=7cm, height=7cm,
  ]
    % Indifference curves (Cobb-Douglas: x*y = k)
    \addplot[thick, domain=0.5:5.5, samples=100] {1/x} node[right] {$U_1$};
    \addplot[thick, domain=0.8:5.5, samples=100] {2.5/x} node[right] {$U_2$};
    \addplot[thick, domain=1.2:5.5, samples=100] {5/x} node[right] {$U_3$};
    % Budget constraint
    \addplot[thick, red] coordinates {(0,5) (5,0)} node[right] {BC};
  \end{axis}
\end{tikzpicture}
```

### 3. Game Theory — Normal Form (2x2)
```latex
\begin{tikzpicture}
  % 2x2 payoff matrix using tikz nodes
  \matrix (m) [matrix of nodes,
    nodes={minimum width=2cm, minimum height=1.2cm, align=center,
           draw, font=\small},
    column sep=-\pgflinewidth,
    row sep=-\pgflinewidth] {
      & Player 2: L & Player 2: R \\
    Player 1: U & 3, 3 & 0, 4 \\
    Player 1: D & 4, 0 & 1, 1 \\
  };
\end{tikzpicture}
```

### 4. IS-LM Model
```latex
\begin{tikzpicture}
  \begin{axis}[
    xlabel={Output $Y$}, ylabel={Interest Rate $r$},
    xmin=0, xmax=10, ymin=0, ymax=10,
    axis lines=left, width=8cm, height=7cm,
  ]
    \addplot[thick, blue, domain=1:9] {10 - x} node[right] {$IS$};
    \addplot[thick, red, domain=1:9] {x} node[right] {$LM$};
    \addplot[dashed] coordinates {(5,0) (5,5)};
    \addplot[dashed] coordinates {(0,5) (5,5)};
  \end{axis}
\end{tikzpicture}
```

### 5. Causal Diagram (DAG)
```latex
\begin{tikzpicture}[node distance=2.5cm, every node/.style={circle, draw}]
  \node (X) {$X$};
  \node (Y) [right of=X] {$Y$};
  \node (Z) [above of=X, xshift=1.25cm] {$Z$};
  \draw[->, thick] (X) -- (Y) node[midway, below] {$\beta$};
  \draw[->, dashed, gray] (Z) -- (X);
  \draw[->, dashed, gray] (Z) -- (Y);
\end{tikzpicture}
```

---

## Step-by-Step Instructions

1. **Identify the diagram type** from the user's description.
2. **Choose the appropriate template** from above, or construct from scratch.
3. **Adapt parameters:**
   - Axis labels and ranges
   - Curve equations and parameter values
   - Node labels, colors, and annotations
4. **Check for common issues:**
   - Are axis labels in sentence case with units?
   - Are equilibria/intersection points marked?
   - Is the diagram size appropriate (7cm × 7cm for slides)?
   - Does `bg = "transparent"` apply if for Beamer slides?
5. **Wrap in appropriate environment** (`frame`, `figure`, or standalone).

---

## TikZ Visual Quality Rules

- Use semantic colors: blue = supply/firm, red = demand/consumer, green = social welfare
- Always label curves and equilibria clearly
- Use `node[above]`, `node[right]` for labels to avoid overlap
- Use `dashed` lines for equilibrium projections to axes
- Font size should be legible at slide size (use `\footnotesize` max reduction)
- Arrows should be `->` or `<->` as appropriate (not bare lines for directed relationships)
