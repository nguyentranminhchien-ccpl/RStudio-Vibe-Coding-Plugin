# Tests for Nominal Variables (Independence)

Independence tests analyze the relationship between two nominal variables organized in a contingency matrix (e.g., Treatment Group vs. Survival status).

## Chi-square Test of Independence
For large contingency tables.
```R
# Enter data as a matrix
Table = matrix(c(10, 15, 20, 25), nrow=2, byrow=TRUE)
rownames(Table) = c("Treated", "Control")
colnames(Table) = c("Survived", "Died")

chisq.test(Table, correct=TRUE) # Yates' correction applied for 2x2
```
*   **Post-hoc (Pairwise comparison):**
    For larger matrices (e.g. 3x2), use pairwise tests with FDR adjustments:
    ```R
    library(rcompanion)
    pairwiseNominalIndependence(Table, method="fdr")
    ```

## G-test of Independence
Alternative to Chi-square, often applied in genetics and ecology.
```R
library(DescTools)
Table = matrix(c(10, 15, 20, 25), nrow=2, byrow=TRUE)
GTest(Table, correct="williams")
```

## Fisher's Exact Test
Preferred for small sample sizes where any expected cell count is less than 5.
```R
Table = matrix(c(4, 1, 2, 5), nrow=2, byrow=TRUE)
fisher.test(Table)
```

## McNemar's Test
Used for paired nominal data (e.g., classification "Healthy"/"Sick" before and after treatment on the same subjects).
```R
# Table of paired observations
Table = matrix(c(15, 5, 2, 10), nrow=2, byrow=TRUE)
mcnemar.test(Table, correct=TRUE)
```

## Cochran-Mantel-Haenszel (CMH) Test
Used to test independence of two nominal variables repeated across different groups or layers (3-dimensional tables).
```R
# Data structure: 2 x 2 x K array
# Rows: Treatment (Active, Placebo)
# Cols: Outcome (Success, Failure)
# Layers: Center/Hospital (1, 2, 3...)
Hospital.Array = array(c(10, 5, 2, 12,  # Center 1
                         15, 4, 3, 10), # Center 2
                       dim = c(2, 2, 2))
mantelhaen.test(Hospital.Array)
```
