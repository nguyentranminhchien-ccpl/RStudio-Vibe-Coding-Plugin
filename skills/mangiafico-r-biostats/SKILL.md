---
name: mangiafico-r-biostats
description: Expert guidance for performing biostatistics in R following the patterns of Salvatore Mangiafico's "An R Companion for the Handbook of Biological Statistics". Use this skill to select appropriate statistical tests, implement them with idiomatic R code, and validate model assumptions.
allowed-tools:
  - Read
  - Grep
argument-hint: [topic, test name, or reference file]
---

# R Biostatistics (Mangiafico Companion)

This skill provides a structured approach to biological statistics in R, focusing on the workflows and packages recommended in Salvatore Mangiafico's "An R Companion for the Handbook of Biological Statistics".

## Core Workflow

1.  **Data Preparation**: Embed data using the datalines pattern `read.table(textConnection(Input))` or load from CSV. Ensure factor columns are explicitly defined.
2.  **Exploratory Data Analysis**: Use `FSA::Summarize` for group-wise statistics and `boxplot()` for initial visualization.
3.  **Test Selection**: Choose the test based on variable types (Nominal vs. Measurement) and sample size (use Exact vs. Asymptotic).
4.  **Modeling & Testing**: Fit models using `lm()`, `glm()`, or specific test functions.
5.  **Validation**: ALWAYS check residuals (`hist()` and `plot(fitted, residuals)`) for parametric tests.
6.  **Post-hoc Analysis**: Use `emmeans` or `agricolae` for pairwise comparisons with p-value adjustments.

## Topic Index

Consult these reference files for specific procedures:

- **R Basics & Setup**: [01_introduction.md](references/01_introduction.md) — load data, packages, contrasts.
- **Nominal Variables (Goodness-of-Fit)**: [02_nominal_gof.md](references/02_nominal_gof.md) — Chi-square, G-test, Exact multinomial, Repeated G-tests.
- **Nominal Variables (Independence)**: [03_nominal_independence.md](references/03_nominal_independence.md) — Chi-square, G-test, Fisher's Exact, McNemar, CMH test.
- **Descriptive Stats & Confidence Limits**: [04_descriptive_stats.md](references/04_descriptive_stats.md) — mean, geometric mean, SD, standard error, binomial CI, bootstrapping.
- **t-tests & One-way ANOVA**: [05_anova.md](references/05_anova.md) — t-tests, one-way ANOVA, Kruskal-Wallis, permutation tests, post-hoc tests.
- **Advanced ANOVA (Two-way, Nested, Mixed Models)**: [06_advanced_anova.md](references/06_advanced_anova.md) — Two-way ANOVA, nested ANOVA, random effects, Type I/II/III sum of squares.
- **Correlation & Linear Regression**: [07_regression.md](references/07_regression.md) — Pearson/Spearman correlation, simple/multiple regression, polynomial regression.
- **Logistic Regression & Multiple Tests**: [08_logistic_multiple.md](references/08_logistic_multiple.md) — simple/multiple logistic regression, ANCOVA, general emmeans contrasts.
- **Specialized Analyses (Cate-Nelson)**: [09_specialized.md](references/09_specialized.md) — Cate-Nelson model, avoiding R coding pitfalls.

## Supporting Resources

- **Glossary of Terms**: [glossary.md](references/glossary.md) — key terminology.
- **Reusable R Patterns**: [patterns.md](references/patterns.md) — boilerplate templates.
- **Quick Reference Cheatsheet**: [cheatsheet.md](references/cheatsheet.md) — decision matrix.

## Preferred R Libraries
`rcompanion`, `FSA`, `car`, `emmeans`, `multcomp`, `DescTools`, `ggplot2`, `coin`, `XNomial`, `agricolae`, `nlme`, `Rmisc`, `boot`.
