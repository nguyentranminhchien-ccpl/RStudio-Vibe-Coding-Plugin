# Data Tidying with tidyr

Tidy data requirements: each variable is a column, each observation is a row, and each value is a single cell.

## Pivoting Data
*   **`pivot_longer()` (Wide to Long):**
    Combine multiple columns representing the same variable under different levels (e.g. `Year2020`, `Year2021`).
    ```R
    billboard |> 
      pivot_longer(
        cols = starts_with("wk"),
        names_to = "week",
        values_to = "rank",
        values_drop_na = TRUE
      )
    ```
*   **`pivot_wider()` (Long to Wide):**
    Spread observations split across rows back into columns.
    ```R
    table2 |> 
      pivot_wider(
        names_from = type,
        values_from = count
      )
    ```

## Separating & Uniting Columns (tidyr 1.3.0+)
*   **`separate_wider_delim()`:** Split a column into multiple columns based on a delimiter character.
    ```R
    # Split code "US-2026" into Country and Year
    Data |> 
      separate_wider_delim(
        cols = code,
        delim = "-",
        names = c("country", "year")
      )
    ```
*   **`unite()`:** Combine multiple columns into one.
    ```R
    # Combine Century and Year into Year4
    Data |> 
      unite(col = "Year4", century, year, sep = "")
    ```
