# Reproducible Reporting with Quarto

Quarto is a unified authoring system for data science combining text, executable code, and visual outputs.

## Quarto Basics
A Quarto file (`.qmd`) contains three main elements:
1.  **YAML Header:** Structured metadata at the top of the file enclosed in `---`.
2.  **Markdown Prose:** Explanations and documentation.
3.  **Code Chunks:** Computations and plot renders.

## YAML Header Configuration
```yaml
---
title: "Data Science Report"
author: "Scientist"
format:
  html:
    toc: true
    code-fold: true
    theme: cosmo
---
```

## Code Chunk Options (`#|` syntax)
Control chunk behavior using comments starting with `#|`:
*   `label`: Unique identifier for the chunk.
*   `warning`: `false` hides warning messages in the output.
*   `message`: `false` hides package load messages.
*   `echo`: `false` hides source code in the output.
*   `eval`: `false` compiles text but does not run the code.
*   `fig-width`, `fig-height`: Set plot dimensions.

Example Quarto chunk:
````markdown
```{r}
#| label: plot-diamonds
#| warning: false
#| message: false
#| fig-width: 6
#| fig-height: 4

library(ggplot2)
ggplot(diamonds, aes(x = carat, y = price)) +
  geom_point(alpha = 0.2)
```
````

## Multi-format Renders
Quarto outputs can render to:
*   HTML (`format: html`)
*   PDF (`format: pdf` - requires LaTeX setup like TinyTeX)
*   MS Word (`format: docx`)
*   Dashboards (`format: dashboard`)
