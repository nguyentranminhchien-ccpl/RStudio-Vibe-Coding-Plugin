# R Biostatistics Patterns

This reference file contains reusable templates for standard biostatistical workflows in R.

## Inline Data Entry
Use this pattern to embed datasets directly into R scripts for reproducibility.
```R
Input = ("
Group Value
Control 12.3
Control 14.5
Control 11.2
Treated 15.6
Treated 18.2
Treated 16.1
")
Data = read.table(textConnection(Input), header=TRUE)
Data$Group = factor(Data$Group)
```

## Complete One-way ANOVA Workflow
Fits a model, checks assumptions, extracts ANOVA tables, performs post-hoc tests, and outputs compact letter displays.
```R
# 1. Fit Model
model = lm(Value ~ Group, data=Data)

# 2. Check Homogeneity of Variance
bartlett.test(Value ~ Group, data=Data)

# 3. Check Residuals
par(mfrow=c(1,2))
hist(residuals(model), main="Residuals Histogram")
plot(fitted(model), residuals(model), main="Fitted vs. Residuals")

# 4. Extract ANOVA (Type II SS)
library(car)
Anova(model, type="II")

# 5. Post-hoc Least-squares Means
library(emmeans)
marginal = emmeans(model, ~ Group)
pairs(marginal, adjust="tukey")

# 6. Compact Letter Display
library(multcomp)
cld(marginal, Letters=letters)
```

## Binary Logistic Regression Workflow
```R
# 1. Fit Generalized Linear Model
model = glm(Survival ~ Dose + Age, data=Data, family="binomial")

# 2. Extract Coefficients and Confidence Intervals as Odds Ratios
OddsRatios = exp(coef(model))
ConfidenceIntervals = exp(confint(model))
cbind(OddsRatios, ConfidenceIntervals)

# 3. Evaluate Goodness-of-Fit (Pseudo R-squared)
library(rcompanion)
nagelkerke(model)
```
