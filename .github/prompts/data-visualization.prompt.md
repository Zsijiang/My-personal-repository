---
mode: 'agent'
description: 'Create publication-ready data visualizations using R and ggplot2. Covers all standard chart types with proper labeling, export settings, and Beamer compatibility.'
---

# Data Visualization

Create publication-quality data visualizations using R and ggplot2 for academic papers and lecture slides.

## Setup

```r
library(tidyverse)
library(ggplot2)

# Optional but recommended
library(scales)      # axis formatting
library(patchwork)   # combining plots
library(viridis)     # color-blind-friendly palettes
library(ggtext)      # rich text in labels

# Project theme (customize as needed)
theme_project <- function() {
  theme_minimal(base_size = 12) +
  theme(
    panel.grid.minor = element_blank(),
    plot.title = element_text(face = "bold"),
    axis.title = element_text(size = 11),
    legend.position = "bottom",
    plot.caption = element_text(size = 9, color = "gray50")
  )
}
```

---

## Chart Types

### Bar Chart
```r
ggplot(data, aes(x = category, y = value, fill = group)) +
  geom_col(position = "dodge") +
  scale_fill_manual(values = c("#1f77b4", "#d62728")) +
  labs(x = NULL, y = "Value", title = "Title",
       caption = "Source: [Source]. Notes: [Notes].") +
  theme_project() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```

### Line Chart (Time Series)
```r
ggplot(data, aes(x = year, y = value, color = group, linetype = group)) +
  geom_line(linewidth = 1) +
  geom_point(size = 2) +
  scale_color_manual(values = c("#1f77b4", "#d62728")) +
  scale_x_continuous(breaks = seq(2000, 2020, 5)) +
  labs(x = "Year", y = "Outcome", title = "Time Trend",
       color = NULL, linetype = NULL) +
  theme_project()
```

### Scatter Plot
```r
ggplot(data, aes(x = x_var, y = y_var, color = group)) +
  geom_point(alpha = 0.6, size = 2) +
  geom_smooth(method = "lm", se = TRUE) +
  labs(x = "X variable (units)", y = "Y variable (units)",
       title = "Relationship between X and Y") +
  theme_project()
```

### Histogram / Density
```r
ggplot(data, aes(x = variable, fill = group)) +
  geom_density(alpha = 0.5, color = NA) +
  scale_fill_manual(values = c("#1f77b4", "#d62728")) +
  labs(x = "Variable (units)", y = "Density",
       fill = NULL) +
  theme_project()
```

### Heatmap (Correlation Matrix)
```r
library(reshape2)
cor_matrix <- cor(data[, numeric_vars], use = "pairwise.complete.obs")
melt(cor_matrix) %>%
  ggplot(aes(x = Var1, y = Var2, fill = value)) +
  geom_tile() +
  geom_text(aes(label = round(value, 2)), size = 3) +
  scale_fill_gradient2(low = "#d62728", mid = "white", high = "#1f77b4",
                       midpoint = 0, limits = c(-1, 1)) +
  labs(x = NULL, y = NULL, fill = "Correlation") +
  theme_project() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))
```

---

## Export Settings

Always export with explicit dimensions:

```r
# For full-width slide (Beamer/Quarto)
ggsave("output/figures/FILENAME.pdf", width = 8, height = 5, bg = "transparent")
ggsave("output/figures/FILENAME.png", width = 8, height = 5, bg = "transparent", dpi = 300)

# For half-width (two-column slide)
ggsave("output/figures/FILENAME.pdf", width = 4, height = 4, bg = "transparent")
```

---

## Quality Checklist

Before finalizing any figure:

- [ ] Axis labels in sentence case with units
- [ ] Caption states: data source, sample period, notes on methodology
- [ ] Legend is self-explanatory (no variable names, use descriptions)
- [ ] Color-blind-friendly palette (test with viridis or manual palette)
- [ ] `bg = "transparent"` for Beamer compatibility
- [ ] Both PDF (vector) and PNG (raster) exported
- [ ] Dimensions explicitly set in `ggsave()`
- [ ] No hardcoded values — use variables for date ranges, sample restrictions

---

## Combining Plots

```r
library(patchwork)

p1 <- ggplot(...) + ...
p2 <- ggplot(...) + ...

# Side by side
(p1 | p2) + plot_annotation(title = "Combined Figure")

# Stacked
(p1 / p2) + plot_layout(heights = c(2, 1))
```
