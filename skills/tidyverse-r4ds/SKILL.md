---
name: tidyverse-r4ds
description: Expert guidance for data science in R using the Tidyverse, based on "R for Data Science (2e)" by Hadley Wickham et al. Use this skill for data visualization (ggplot2), transformation (dplyr), tidying (tidyr), import (readr), and workflow management (Quarto).
allowed-tools:
  - Read
  - Grep
argument-hint: [topic, function name, or chapter number]
---

# Tidyverse & R for Data Science

This skill provides a comprehensive guide to modern data science in R, following the principles and patterns of the Tidyverse as described in "R for Data Science (2nd Edition)".

## Core Philosophy: Tidy Data
Data should be organized such that each variable is a column, each observation is a row, and each cell contains a single value. This consistency allows Tidyverse tools to work together seamlessly.

## Key Packages
- **`ggplot2`**: Data visualization using the grammar of graphics.
- **`dplyr`**: Data transformation (filtering, mutating, summarizing).
- **`tidyr`**: Data tidying (pivoting, nesting).
- **`readr`**: Data import (CSV, TSV, etc.).
- **`stringr`**: String manipulation.
- **`forcats`**: Factor manipulation.
- **`lubridate`**: Dates and times.

## Topic Index

Consult these reference files for specific procedures:

- **Data Visualization**: [01_visualization.md](references/01_visualization.md) — grammar of graphics, layered geoms, faceting, communication styling.
- **Data Transformation**: [02_transformation_basics.md](references/02_transformation_basics.md) — native pipe |>, core dplyr verbs, column-wise across(), group-wise mutate.
- **Data Types (Logicals, Numbers, Strings, Factors, Dates)**: [03_data_types.md](references/03_data_types.md) — logical vectors, stringr regex, forcats reordering, lubridate dates.
- **Data Import**: [04_data_import.md](references/04_data_import.md) — readr CSV parsing options, readxl, dbplyr SQL backend.
- **Data Tidying**: [05_data_tidying.md](references/05_data_tidying.md) — pivot_longer, pivot_wider, separate_wider_delim.
- **Workflow & Quarto**: [06_workflow_quarto.md](references/06_workflow_quarto.md) — Quarto basics, YAML header, chunk options, rendering formats.

## Supporting Resources

- **Glossary of Terms**: [glossary.md](references/glossary.md) — key terminology definitions.
- **Tidyverse Design Patterns**: [patterns.md](references/patterns.md) — boilerplate workflows.
- **Quick Reference Cheatsheet**: [cheatsheet.md](references/cheatsheet.md) — quick syntax lookup.

## Preferred Workflow
Use RStudio Projects, organize files with clear naming conventions, and use Quarto for reproducible reporting. Chain operations using the native pipe `|>`.
