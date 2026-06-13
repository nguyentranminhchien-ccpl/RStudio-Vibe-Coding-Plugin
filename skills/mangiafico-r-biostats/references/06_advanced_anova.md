# Advanced ANOVA (Two-way, Nested, Mixed Models)

Covers models with multiple factors, hierarchical designs, and balanced vs. unbalanced data considerations.

## Type I, II, and III Sums of Squares
R's default `anova()` uses sequential (Type I) sum of squares, where order of terms matters. For unbalanced designs or to mimic SAS defaults, use Type II or Type III:
*   **Type I (Sequential):** `anova(lm(Y ~ A * B))`
*   **Type II (Marginality-preserving):** Used when interactions are negligible.
*   **Type III (Partial):** Evaluates each factor in presence of all other factors, including interactions. **Contrasts must be changed to sum-to-zero for Type III to be mathematically correct in R:**
```R
# 1. Set contrasts
options(contrasts = c("contr.sum", "contr.poly"))

# 2. Fit model
model = lm(Y ~ A * B, data=Data)

# 3. Compute Type III SS
library(car)
Anova(model, type="III")

# 4. Reset contrasts to default
options(contrasts = c("contr.treatment", "contr.poly"))
```

## Two-way ANOVA
Tests effects of two factors and their interaction.
```R
model = lm(Y ~ A * B, data=Data)
library(car)
Anova(model, type="II")
```
*   **Interaction Plots:**
    ```R
    interaction.plot(x.factor=Data$A, trace.factor=Data$B, response=Data$Y)
    ```

## Nested ANOVA
Hierarchical designs (e.g., replicates nested within treatments, or samples nested within lakes).
*   **Fixed Effects Nested ANOVA:**
    ```R
    model = lm(Y ~ Treatment + Treatment:Replicate, data=Data)
    anova(model)
    ```
*   **Mixed Effects Nested ANOVA (Random Block / Nested Factor):**
    Using the `nlme` package, treating nesting levels as random effects.
    ```R
    library(nlme)
    model = lme(Y ~ Treatment, random = ~ 1 | Location/Sublocation, data=Data)
    summary(model)
    ```
