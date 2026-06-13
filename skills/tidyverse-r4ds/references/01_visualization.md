# Data Visualization with ggplot2

Guides on creating data visualizations using the grammar of graphics in R.

## The Layered Grammar of Graphics
A plot is built from multiple layers:
1.  **Data:** The dataset containing the variables to plot.
2.  **Mapping (Aesthetics):** How variables map to visual properties (`aes(x, y, color, size, shape)`).
3.  **Geoms:** Geometric objects that represent data points (`geom_point`, `geom_bar`, `geom_line`, `geom_boxplot`).
4.  **Stats:** Statistical transformations (e.g. binning for histograms, fitting lines for `geom_smooth`).
5.  **Position:** Adjusting positions of geoms (e.g., `position = "dodge"` or `"fill"` for bars).
6.  **Coordinate System:** `coord_flip()`, `coord_polar()`.
7.  **Faceting:** Small multiples (`facet_wrap`, `facet_grid`).
8.  **Themes:** Plot styling (`theme_minimal()`, `theme_classic()`).

## Standard Plot Templates
*   **Scatterplot with Smoothed Line:**
    ```R
    ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
      geom_point(mapping = aes(color = class)) + 
      geom_smooth(se = FALSE)
    ```
*   **Bar Chart (Counts):**
    ```R
    ggplot(data = diamonds, mapping = aes(x = cut)) +
      geom_bar()
    ```
*   **Bar Chart (Identity - Pre-computed values):**
    ```R
    ggplot(data = demo_data, mapping = aes(x = Category, y = Value)) +
      geom_col()
    ```
*   **Faceting ribbon (1D):**
    ```R
    ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
      geom_point() +
      facet_wrap(~ class, nrow = 2)
    ```
*   **Faceting grid (2D):**
    ```R
    ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
      geom_point() +
      facet_grid(drv ~ cyl)
    ```

## Communication & Fine-Tuning
Add labels, adjust scales, and tune themes for publication-ready figures.
```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) +
  geom_point(aes(color = class)) +
  geom_smooth(se = FALSE) +
  labs(
    title = "Fuel Efficiency vs. Engine Size",
    subtitle = "Data from 1999 to 2008 for 38 popular models of cars",
    x = "Engine displacement (L)",
    y = "Highway fuel economy (mpg)",
    color = "Car class",
    caption = "Source: https://fueleconomy.gov"
  ) +
  scale_color_brewer(palette = "Set1") +
  theme_minimal()
```

## Saving Plots
Always save plots with explicit dimensions:
```R
ggsave("my-plot.png", width = 8, height = 6, dpi = 300)
```
