# Descriptive Statistics and Confidence Limits

Summary statistics summarize central tendency and dispersion, while confidence limits quantify parameter uncertainty.

## Central Tendency
*   **Arithmetic Mean:** `mean(x, na.rm=TRUE)`.
*   **Geometric Mean:** Correct for log-normal data (e.g., bacterial counts).
    ```R
    library(psych)
    geometric.mean(x)
    ```
*   **Median & Mode:**
    ```R
    median(x, na.rm=TRUE)
    library(DescTools)
    Mode(x)
    ```

## Dispersion
*   **Standard Deviation & Variance:** `sd(x)`, `var(x)`.
*   **Coefficient of Variation (CV%):**
    ```R
    library(DescTools)
    CoeffVar(x, na.rm=TRUE) * 100
    ```
*   **Standard Error of the Mean (SEM):**
    ```R
    sd(x)/sqrt(sum(!is.na(x)))
    ```

## Grouped Descriptive Statistics
```R
library(FSA)
Summarize(Value ~ Group, data=Data)
```

## Confidence Limits (CL)
*   **Normal-based Mean CI:**
    ```R
    t.test(x)$conf.int
    ```
*   **Grouped Data Mean CI:**
    ```R
    library(Rmisc)
    summarySE(data=Data, measurevar="Value", groupvars="Group")
    ```
*   **Proportion Confidence Intervals:**
    Calculate CI for binomial successes using Agresti-Coull or Wilson methods:
    ```R
    library(DescTools)
    BinomCI(x=15, n=50, conf.level=0.95, method="agresti-coull")
    ```
*   **Bootstrapped Confidence Intervals:**
    Non-parametric bootstrap for arbitrary estimators:
    ```R
    library(boot)
    boot_func = function(data, indices) { mean(data[indices]) }
    results = boot(data=x, statistic=boot_func, R=1000)
    boot.ci(results, type="bca")
    ```
