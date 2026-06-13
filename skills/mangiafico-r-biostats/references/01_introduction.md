# Introduction to R for Biostatistics (Mangiafico)

This guide covers setup, basic workflow, package installation, data entry, and project hygiene guidelines from Salvatore Mangiafico's biostatistics companion.

## R Coding Philosophy
*   **Assignment Operator:** Use the `=` operator or standard `<-` (the author prefers `=` for clarity).
*   **Data Types:** Common structures include vectors, matrices, factors, and data frames.
*   **Contrasts for Type III sums of squares:** R's default contrast scheme is treatment contrasts. When performing Type III ANOVA, the contrasts must be changed:
    ```R
    options(contrasts = c("contr.sum", "contr.poly"))
    ```
    To reset to default behavior afterwards:
    ```R
    options(contrasts = c("contr.treatment", "contr.poly"))
    ```

## Core Packages
*   `rcompanion`: Author's package containing helper functions for Cate-Nelson, pseudo R-squared, pairwise nominal tests, and plotting.
*   `car`: Standard package for Type II and Type III Analysis of Variance (`Anova`).
*   `DescTools`: Comprehensive package for G-tests, descriptive statistics, and confidence intervals.
*   `FSA`: Fisheries Stock Assessment package, used for data summarizing (`Summarize`) and post-hoc Dunn tests (`dunnTest`).
*   `emmeans`: Used to compute estimated marginal means (least-squares means) and pairwise contrasts.

## Standard Data Entry Pattern
For reproducible examples, use `read.table` with a text connection. Factors should be explicitly defined:
```R
Input = ("
Group Value
2pm    69
2pm    70
2pm    66
2pm    63
2pm    68
5pm    68
5pm    62
5pm    67
5pm    68
")
Data = read.table(textConnection(Input), header=TRUE)
Data$Group = factor(Data$Group)
str(Data)
```

## Basic Biostatistical Workflow
1.  **Environment Check:** Reset options and load packages:
    ```R
    if(!require(rcompanion)){install.packages("rcompanion")}
    library(rcompanion)
    ```
2.  **Inspect Data Structure:** Check dimensions (`dim(Data)`), column names (`names(Data)`), and variable types (`str(Data)`).
3.  **Descriptive Summaries:** Run `FSA::Summarize` or `DescTools::Desc`.
4.  **Visualize Assumptions:** Plot data distributions using histograms (`hist(Data$Value)`) and box plots (`boxplot(Value ~ Group, data=Data)`).
5.  **Hypothesis Testing:** Fit regression or ANOVA model (`lm` or `glm`).
6.  **Model Validation:** Validate residuals using `plot(fitted(model), residuals(model))`.
