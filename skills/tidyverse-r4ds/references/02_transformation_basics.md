# Data Transformation with dplyr

Verbs for filtering rows, selecting columns, reordering, creating columns, and summarizing groups.

## The Pipe `|>`
Chain multiple operations cleanly. The output of one function becomes the first argument of the next.
```R
# Standard Tidyverse pipeline
flights |> 
  filter(dest == "IAH") |> 
  group_by(year, month, day) |> 
  summarize(arr_delay = mean(arr_delay, na.rm = TRUE))
```

## Core Verbs
1.  **`filter()`:** Select rows based on conditions.
    ```R
    flights |> filter(dep_delay > 120 & dest %in% c("IAH", "HOU"))
    ```
2.  **`arrange()`:** Sort rows by one or more variables.
    ```R
    flights |> arrange(desc(dep_delay), arr_delay)
    ```
3.  **`distinct()`:** Keep unique rows.
    ```R
    flights |> distinct(origin, dest, .keep_all = TRUE)
    ```
4.  **`mutate()`:** Add new columns or modify existing ones.
    ```R
    flights |> mutate(gain = dep_delay - arr_delay, .before = 1)
    ```
5.  **`select()`:** Keep or drop columns.
    ```R
    flights |> select(year:day, starts_with("arr_"))
    ```
6.  **`summarize()`:** Compute group-wise summaries.
    ```R
    flights |> 
      group_by(month) |> 
      summarize(
        count = n(),
        delay = mean(dep_delay, na.rm = TRUE)
      )
    ```

## Column-wise Operations using `across()`
Apply the same function to multiple columns simultaneously. This is highly recommended when transforming many variables to the same type (e.g. converting numeric codes to factors).
```R
# Converting multiple variable columns to factor with labels
Data = Data |> 
  mutate(across(c(GioiTinh, TienSu, KetQua), 
                ~factor(.x, levels = c(0, 1), labels = c("Không", "Có"))))
```

## Grouping and `.by` (dplyr 1.1.0+)
Instead of using `group_by()` and `ungroup()`, you can perform one-off grouped operations using the `.by` argument in `mutate()` and `summarize()`:
```R
# Mutate with group-wise calculation
flights |> 
  mutate(mean_delay = mean(dep_delay, na.rm = TRUE), .by = month)
```
