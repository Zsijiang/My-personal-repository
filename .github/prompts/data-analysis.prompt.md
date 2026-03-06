---
mode: 'agent'
description: 'End-to-end R data analysis workflow from exploration through regression to publication-ready tables and figures. For economics empirical research.'
---

# Data Analysis Workflow

Run an end-to-end data analysis in R: load, explore, analyze, and produce publication-ready output.

## Constraints

- **Follow R code conventions** in `.github/copilot-instructions.md`
- **Save all scripts** to `scripts/R/` with descriptive names
- **Save all outputs** (figures, tables, RDS) to `output/`
- **Use `saveRDS()`** for every computed object
- **Use project theme** for all figures
- **Run code review** on the generated script before presenting results

---

## Workflow Phases

### Phase 1: Setup and Data Loading

1. Create R script with proper header (title, author, purpose, inputs, outputs)
2. Load required packages at top (`library()`, never `require()`)
3. Set seed once at top: `set.seed(42)`
4. Load and inspect the dataset

```r
# ============================================================
# [Descriptive Title]
# Purpose: [What this script does]
# Inputs:  [Data files]
# Outputs: [Figures, tables, RDS files]
# ============================================================

library(tidyverse)
library(fixest)
library(modelsummary)

set.seed(42)

dir.create("output/analysis", recursive = TRUE, showWarnings = FALSE)

data <- read_csv("data/FILENAME.csv")
glimpse(data)
summary(data)
```

### Phase 2: Exploratory Data Analysis

- **Summary statistics:** `summary()`, missingness rates, variable types
- **Distributions:** Histograms for key continuous variables
- **Relationships:** Scatter plots, correlation matrices
- **Time patterns:** If panel data, plot trends over time
- **Group comparisons:** If treatment/control, compare pre-treatment means

Save all diagnostic figures to `output/diagnostics/`.

### Phase 3: Main Analysis

**Regression analysis:**
```r
# Cross-sectional OLS
m1 <- lm(y ~ x + controls, data = data)
m1_robust <- lm_robust(y ~ x + controls, data = data, se_type = "HC3")

# Panel with fixed effects (use fixest)
m2 <- feols(y ~ x + controls | entity + time, data = panel_data,
            cluster = ~entity)

# Two-way fixed effects DiD
m3 <- feols(y ~ treat_post | entity + time, data = panel_data,
            cluster = ~entity)
```

**Always:**
- Start simple (no controls), progressively add controls
- Use `fixest` for panel data
- Cluster at the appropriate level (document why)
- Report multiple specifications

### Phase 4: Publication-Ready Output

**Regression tables:**
```r
# modelsummary (preferred)
modelsummary(
  list("(1)" = m1, "(2)" = m2, "(3)" = m3),
  stars = c("*" = 0.1, "**" = 0.05, "***" = 0.01),
  gof_map = c("nobs", "r.squared", "adj.r.squared"),
  output = "output/tables/main_results.tex"
)

# Also save HTML for quick viewing
modelsummary(
  list("(1)" = m1, "(2)" = m2, "(3)" = m3),
  output = "output/tables/main_results.html"
)
```

**Figures:**
```r
ggsave("output/figures/main_figure.pdf", width = 7, height = 4, bg = "transparent")
ggsave("output/figures/main_figure.png", width = 7, height = 4, bg = "transparent", dpi = 300)
```

### Phase 5: Save and Review

```r
# Save key objects
saveRDS(m3, "output/rds/main_model.rds")
saveRDS(data_clean, "output/rds/clean_data.rds")
```

---

## Script Structure Template

```r
# ============================================================
# [Descriptive Title]
# Purpose: [What this script does]
# Inputs:  [Data files]
# Outputs: [Figures, tables, RDS files]
# ============================================================

# 0. Setup ----
library(tidyverse)
library(fixest)
library(modelsummary)
library(estimatr)

set.seed(42)

dir.create("output/analysis", recursive = TRUE, showWarnings = FALSE)

# 1. Data Loading ----

# 2. Exploratory Analysis ----

# 3. Main Analysis ----

# 4. Tables and Figures ----

# 5. Export ----
```

---

## Important

- **Reproduce, don't guess.** If the user specifies a regression, run exactly that.
- **Show your work.** Print summary statistics before jumping to regression.
- **Check for issues.** Look for multicollinearity, outliers, perfect prediction.
- **Use relative paths.** All paths relative to repository root.
- **No hardcoded values.** Use variables for sample restrictions, date ranges, etc.
- **Document clustering.** Always comment why you cluster at a particular level.
