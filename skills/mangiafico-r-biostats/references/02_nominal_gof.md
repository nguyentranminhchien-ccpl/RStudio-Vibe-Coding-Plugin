# Tests for Nominal Variables (Goodness-of-Fit)

Goodness-of-fit (GoF) tests compare observed counts in one nominal variable against expected proportions derived from a null hypothesis (e.g., Mendelian ratios like 9:3:3:1).

## Exact Test of Goodness-of-Fit
Used when sample size is small (N < 20 or expected cell count < 5).
*   **Two Categories (Exact Binomial Test):**
    ```R
    binom.test(x=5, n=20, p=0.5, alternative="two.sided")
    ```
*   **Three or More Categories (Exact Multinomial Test):**
    Requires the `XNomial` package.
    ```R
    library(XNomial)
    observed = c(5, 10, 15)
    expected = c(1/3, 1/3, 1/3)
    xmulti(observed, expected, detail=3)
    ```

## Chi-square Test of Goodness-of-Fit
For large samples (all expected cell counts > 5).
```R
observed = c(290, 3, 290, 7)
expected = c(0.25, 0.25, 0.25, 0.25)
chisq.test(x=observed, p=expected)
```

## G-test of Goodness-of-Fit
Alternative to Chi-square test, theoretically preferred due to additive properties.
```R
library(DescTools)
observed = c(290, 3, 290, 7)
expected = c(0.25, 0.25, 0.25, 0.25)
# Using Williams' correction for smaller samples
GTest(x=observed, p=expected, correct="williams")
```

## Repeated G-tests of Goodness-of-Fit
Used when you have independent replicates of a goodness-of-fit experiment (e.g. testing the same ratio on different days).
*   Individual G-tests are performed on each replicate.
*   A **Pooled G-test** is run on the summed data.
*   A **Total G-test** sums the individual G statistics.
*   A **Heterogeneity G-test** is computed as $G_{heterogeneity} = G_{total} - G_{pooled}$ to check if replicates differ significantly.
```R
# Example data structure
# Replicate ObservedA ObservedB ExpectedA ExpectedB
# Day1      10        20        0.33      0.67
# Day2      12        18        0.33      0.67
# Check rcompanion package documentation for repeated G-tests workflows.
```
