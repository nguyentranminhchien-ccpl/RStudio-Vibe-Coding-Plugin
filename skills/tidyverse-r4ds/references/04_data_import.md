# Data Import with readr and readxl

Read tabular data from disk into tidy data frames (tibbles).

## Reading CSV/TSV Files (`readr`)
```R
library(readr)
# Read CSV file
Data = read_csv("data.csv")
```
*   **Parsing Options:**
    Control header rows, skip rows, or define NA strings:
    ```R
    Data = read_csv(
      "data.csv",
      skip = 2,
      na = c(".", "NA", "missing")
    )
    ```
*   **Column Type Specifications:**
    Force specific types during reading to avoid parser errors:
    ```R
    Data = read_csv(
      "data.csv",
      col_types = cols(
        ID = col_integer(),
        Date = col_date(format = "%Y-%m-%d"),
        Gender = col_factor(levels = c("M", "F"))
      )
    )
    ```

## Reading Excel Files (`readxl`)
Part of the tidyverse, but must be loaded explicitly.
```R
library(readxl)
# List sheets
excel_sheets("data.xlsx")

# Read specific sheet and range
Data = read_excel("data.xlsx", sheet = "Sheet1", range = "A1:E100")
```

## Reading Databases & Arrow Files
For large datasets that do not fit in memory:
*   `DBI` and `dbplyr` let you write dplyr pipelines that are translated directly to SQL and executed on databases.
*   `arrow` allows reading Parquet files efficiently.
