# Tidyverse Cheatsheet

Quick syntax lookup for common tasks.

## dplyr Verbs
*   `filter(cond)`: Subset rows.
*   `arrange(col)`: Reorder rows.
*   `select(col1:colN)`: Keep/drop columns.
*   `mutate(new = col1 + col2)`: Create/modify columns.
*   `summarize(avg = mean(col))`: Group aggregation.
*   `across(cols, func)`: Apply a function to multiple columns.

## ggplot2 layers
```R
ggplot(data, aes(x, y, color = class)) +
  geom_point() +
  geom_smooth() +
  facet_wrap(~ group) +
  theme_minimal()
```

## stringr functions
*   `str_detect(string, pattern)`: Check if pattern exists.
*   `str_replace(string, pattern, replacement)`: Replace matching pattern.
*   `str_split(string, pattern)`: Split strings.

## lubridate functions
*   `ymd(str)`, `dmy(str)`: Parse strings to date.
*   `floor_date(date, unit)`: Round date down to boundary.
*   `today()`, `now()`: Current date and time.
