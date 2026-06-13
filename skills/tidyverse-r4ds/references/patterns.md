# Tidyverse Design Patterns

boilerplate code templates for typical data science workflows.

## Standard Transformation & Visualization Pipeline
```R
library(tidyverse)

# 1. Load Data
raw_data = read_csv("my_dataset.csv")

# 2. Transform & Clean
clean_data = raw_data |> 
  filter(!is.na(Value)) |> 
  mutate(
    # Recode factors column-wise
    across(c(Status, Group), ~factor(.x)),
    LogValue = log10(Value)
  ) |> 
  arrange(desc(LogValue))

# 3. Aggregate
grouped_summary = clean_data |> 
  group_by(Group) |> 
  summarize(
    Count = n(),
    Mean = mean(Value),
    SD = sd(Value)
  )

# 4. Plot Renders
ggplot(clean_data, aes(x = Group, y = LogValue, fill = Group)) +
  geom_boxplot() +
  labs(
    title = "Log Value Distribution by Group",
    x = "Experimental Group",
    y = "Log10 Value"
  ) +
  theme_minimal()
```

## Reshaping Data (Wide to Long)
```R
# Pivot multiple year-columns into a single year variable
long_data = wide_data |> 
  pivot_longer(
    cols = starts_with("Year_"),
    names_to = "Year",
    names_prefix = "Year_",
    values_to = "Measurement"
  )
```
