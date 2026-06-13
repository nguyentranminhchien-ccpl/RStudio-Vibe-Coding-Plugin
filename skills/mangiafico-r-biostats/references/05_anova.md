# One-way ANOVA and Non-parametric Alternatives

Methods for comparing means or distributions across two or more independent groups.

## Student's t-test
*   **One-sample t-test:** Compare sample mean to a reference value.
    ```R
    t.test(Data$Value, mu=65)
    ```
*   **Two-sample t-test (Equal Variances):**
    ```R
    t.test(Value ~ Group, data=Data, var.equal=TRUE)
    ```
*   **Welch's t-test (Unequal Variances):** Preferred default in R.
    ```R
    t.test(Value ~ Group, data=Data, var.equal=FALSE)
    ```

## Two-sample Permutation Test
Alternative to t-test when normality assumptions are severely violated.
```R
library(coin)
independence_test(Value ~ Group, data=Data)
```

## One-way ANOVA
For comparing three or more group means.
1.  **Check Assumptions:**
    *   Homogeneity of Variance: `bartlett.test(Value ~ Group, data=Data)` or `leveneTest` in `car` package.
2.  **Fit Model:**
    ```R
    model = lm(Value ~ Group, data=Data)
    anova(model) # Type I SS (fine for balanced design)
    ```
3.  **Diagnose Residuals:**
    ```R
    par(mfrow=c(1,2))
    hist(residuals(model))
    plot(fitted(model), residuals(model))
    ```

## Post-hoc Comparisons (ANOVA)
*   **Tukey's HSD:**
    ```R
    library(agricolae)
    HSD.test(model, "Group", console=TRUE)
    ```
*   **Least-Squares Means (EMMeans):**
    ```R
    library(emmeans)
    marginal = emmeans(model, ~ Group)
    pairs(marginal, adjust="tukey")
    ```

## Non-parametric Alternatives
*   **Kruskal-Wallis Test (Three or more groups):**
    ```R
    kruskal.test(Value ~ Group, data=Data)
    ```
*   **Post-hoc Dunn Test:**
    ```R
    library(FSA)
    dunnTest(Value ~ Group, data=Data, method="bh") # Benjamini-Hochberg adjustment
    ```
