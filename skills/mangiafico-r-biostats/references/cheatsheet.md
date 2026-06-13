# R Biostatistics Cheatsheet

Quick reference for selecting and executing statistical tests in R.

## Test Selection Guide

| Dependent Variable | Independent Variable(s) | Assumptions Met? | Parametric Test | Non-Parametric Test |
| :--- | :--- | :--- | :--- | :--- |
| 1 Measurement | 1 Nominal (2 levels) | Yes (Normality, Var) | Student's t-test (`t.test`) | Wilcoxon Rank-Sum (`wilcox.test`) |
| 1 Measurement | 1 Nominal (2 levels) | No (Unequal Var) | Welch's t-test (`t.test`) | Wilcoxon Rank-Sum (`wilcox.test`) |
| 1 Measurement | 1 Nominal (3+ levels) | Yes | One-way ANOVA (`lm` + `Anova`) | Kruskal-Wallis (`kruskal.test`) |
| 1 Measurement | 2 Nominal | Yes | Two-way ANOVA (`lm` + `Anova`) | Scheirer-Ray-Hare (`scheirerRayHare`) |
| 1 Measurement | 1 Measurement | Yes | Linear Regression (`lm`) | Spearman Correlation (`cor.test`) |
| Binary Nominal | 1+ Measurement/Nominal | - | Logistic Regression (`glm`) | - |
| 1 Nominal | expected ratios | - | Chi-square GoF (`chisq.test`) | Exact Binomial (`binom.test`) |
| 2 Nominal | - (Contingency) | - | Chi-square Independence | Fisher's Exact Test (`fisher.test`) |
| 2 Nominal | - (Before/After) | - | McNemar's Test (`mcnemar.test`) | - |

## Quick Command Syntax Reference

```R
# Descriptive Stats
FSA::Summarize(Y ~ X, data=Data)
DescTools::Desc(Data$Y)

# Means Comparison
t.test(Y ~ X, data=Data, var.equal=FALSE) # Welch's t-test
wilcox.test(Y ~ X, data=Data)             # Wilcoxon Rank-Sum

# ANOVA & Post-hoc
model = lm(Y ~ X, data=Data)
car::Anova(model, type="II")
emmeans::emmeans(model, pairwise ~ X, adjust="tukey")

# Correlation & Regression
cor.test(Data$X, Data$Y, method="pearson")
model_reg = lm(Y ~ X, data=Data)
summary(model_reg)

# Logistic Regression
model_log = glm(Y_binary ~ X, data=Data, family="binomial")
exp(coef(model_log)) # Odds Ratios
```
