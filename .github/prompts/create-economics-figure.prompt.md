---
mode: 'agent'
description: 'Create publication-ready economics figures using R and ggplot2. Covers supply/demand charts, regression coefficients plots, panel data visualizations, and DiD event studies.'
---

# Create Economics Figure

Create publication-quality figures for economics research using R and ggplot2. Covers the most common types of figures in empirical economics papers.

## Figure Types

### 1. Coefficient Plot (Point Estimates + Confidence Intervals)

```r
library(tidyverse)
library(ggplot2)

# Assumes a data frame: estimate, conf.low, conf.high, term
ggplot(results_df, aes(x = estimate, y = term)) +
  geom_vline(xintercept = 0, linetype = "dashed", color = "gray50") +
  geom_point(size = 3) +
  geom_errorbarh(aes(xmin = conf.low, xmax = conf.high), height = 0.2) +
  labs(x = "Coefficient estimate", y = NULL,
       title = "Effect of X on Y",
       caption = "Notes: 95% confidence intervals. Standard errors clustered by [unit].") +
  theme_minimal(base_size = 12) +
  theme(panel.grid.minor = element_blank())

ggsave("output/figures/coef_plot.pdf", width = 7, height = 4, bg = "transparent")
ggsave("output/figures/coef_plot.png", width = 7, height = 4, bg = "transparent")
```

### 2. Event Study / Dynamic DiD

```r
library(tidyverse)
library(ggplot2)

# Assumes: event_time (relative time), estimate, conf.low, conf.high
ggplot(event_study_df, aes(x = event_time, y = estimate)) +
  geom_hline(yintercept = 0, linetype = "dashed", color = "gray50") +
  geom_vline(xintercept = -0.5, linetype = "dotted", color = "gray30") +
  geom_ribbon(aes(ymin = conf.low, ymax = conf.high), alpha = 0.2, fill = "steelblue") +
  geom_line(color = "steelblue", linewidth = 1) +
  geom_point(color = "steelblue", size = 2.5) +
  labs(x = "Event time (years relative to treatment)",
       y = "Treatment effect estimate",
       title = "Dynamic Treatment Effect",
       caption = "Notes: 95% confidence intervals. Standard errors clustered by state.") +
  theme_minimal(base_size = 12)

ggsave("output/figures/event_study.pdf", width = 7, height = 4, bg = "transparent")
```

### 3. Binscatter / Partial Scatter Plot

```r
library(tidyverse)
library(binsreg)  # or use manual binning

# Manual binning example
data_binned <- data %>%
  mutate(bin = ntile(x_var, 20)) %>%
  group_by(bin) %>%
  summarise(x_mean = mean(x_var), y_mean = mean(y_residual))

ggplot(data_binned, aes(x = x_mean, y = y_mean)) +
  geom_point(size = 2, color = "steelblue") +
  geom_smooth(method = "lm", color = "red", se = TRUE, linewidth = 0.8) +
  labs(x = "X variable", y = "Y (residualized)",
       title = "Binscatter: Y vs X (conditional on controls)") +
  theme_minimal(base_size = 12)
```

### 4. Map of Treatment Rollout (Panel DiD)

```r
library(tidyverse)
library(sf)

states_sf %>%
  left_join(treatment_timing, by = "state") %>%
  ggplot() +
  geom_sf(aes(fill = as.factor(treat_year)), color = "white", linewidth = 0.3) +
  scale_fill_viridis_d(name = "Treatment Year", na.value = "gray90") +
  labs(title = "Treatment Rollout by State") +
  theme_void(base_size = 12)
```

### 5. Distribution Comparison (Pre/Post or Treatment/Control)

```r
ggplot(data, aes(x = outcome, fill = group)) +
  geom_density(alpha = 0.4, color = NA) +
  scale_fill_manual(values = c("Control" = "steelblue", "Treatment" = "tomato")) +
  labs(x = "Outcome variable", y = "Density",
       title = "Distribution of Outcomes by Group") +
  theme_minimal(base_size = 12) +
  theme(legend.title = element_blank())
```

---

## Step-by-Step Instructions

1. **Identify the figure type** based on the user's request
2. **Adapt the template:**
   - Replace variable names with actual column names
   - Update axis labels with units (e.g., "Log wages (2010 USD)")
   - Update the caption with clustering information
   - Set appropriate axis limits
3. **Apply project theme** if a custom theme is defined
4. **Export settings:**
   - Width: 7–8 inches for single-column, 3.5 inches for half-width
   - Height: 4–5 inches (adjust for aspect ratio)
   - Always export both PDF (vector) and PNG (raster)
   - Set `bg = "transparent"` for Beamer compatibility
5. **Save to** `output/figures/` with a descriptive name

---

## Axis Label Rules

- **Sentence case**, not title case: "Log wages (2010 USD)" not "Log Wages (2010 USD)"
- **Include units** in parentheses: "(pp)" for percentage points, "(log)" for log scale
- **No jargon** in axis labels — write out "Treatment effect estimate" not "β̂"
- **Captions** must state: sample, standard error clustering, confidence level

---

## Color Palette

| Use | Color |
|-----|-------|
| Treatment / Main | `#1f77b4` (steelblue) |
| Control / Comparison | `#d62728` (red) |
| Pre-period | `#aec7e8` (light blue) |
| Post-period | `#ffbb78` (light orange) |
| Neutral / Reference | `gray50` |
