# Working with Data Types

Tidyverse packages tailored for working with specific vectors/classes.

## Logical Vectors
*   **Boolean checks:** `==`, `!=`, `>`, `<`, `%in%`.
*   **Logic gates:** `&` (and), `|` (or), `!` (not), `xor()`.
*   **NA values:** `is.na(x)` checks for missing values. Note that `NA` represents "unknown", so `NA == NA` yields `NA`.
*   **Numeric summaries of logicals:** `sum(df$Delayed)` counts the number of `TRUE` values; `mean(df$Delayed)` returns the proportion of `TRUE` values.

## Numbers
*   **Arithmetic:** `%/%` (integer division), `%%` (modulo/remainder).
*   **Functions:** `round()`, `floor()`, `ceiling()`.
*   **Summaries:** `mean()`, `median()`, `sd()`, `IQR()`.

## Strings (`stringr`)
*   **Length:** `str_length(string)`.
*   **Combine:** `str_c("prefix-", column, sep = "")`.
*   **Substring:** `str_sub(string, start, end)`.
*   **Matching & Regex:**
    ```R
    # Detect pattern
    str_detect(words, "ing$")
    
    # Replace pattern
    str_replace_all(words, "[aeiou]", "-")
    ```

## Factors (`forcats`)
Manage categorical data with fixed levels.
*   **Reordering levels (for plots):**
    ```R
    # Reorder by another variable's value
    fct_reorder(factor_col, numeric_col)
    
    # Reorder by frequency of occurrence
    fct_infreq(factor_col)
    ```
*   **Recoding levels:**
    ```R
    fct_recode(factor_col, "Active" = "1", "Control" = "0")
    ```

## Dates and Times (`lubridate`)
*   **Parsing:** `ymd("2026-06-11")`, `mdy("June 11, 2026")`, `dmy_hms("11-06-2026 15:45:00")`.
*   **Extraction:** `year()`, `month(label = TRUE)`, `mday()`, `wday()`.
*   **Rounding:**
    ```R
    # Round down to the nearest month boundary
    floor_date(Date, unit = "month")
    ```
