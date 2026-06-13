# Logistic Regression and Multiple Comparisons

 logistic regression modeling and general post-hoc pairwise contrast workflows.

## Simple Logistic Regression
Used when the dependent variable is binary nominal (e.g. Success/Failure, Alive/Dead).
```R
# Family must be binomial
model = glm(Survival ~ Dose, data=Data, family="binomial")
summary(model)

# Extract Odds Ratios (OR) and CIs
exp(coef(model))
exp(confint(model))
```

## Multiple Logistic Regression
```R
model = glm(Survival ~ Dose + Age + Gender, data=Data, family="binomial")
summary(model)
```
Assess goodness-of-fit using pseudo R-squared:
```R
library(rcompanion)
nagelkerke(model)
```

## Analysis of Covariance (ANCOVA)
Combines ANOVA and linear regression to compare group means while adjusting for a continuous covariate.
```R
model = lm(Y ~ Covariate + TreatmentGroup, data=Data)
library(car)
Anova(model, type="II")
```

## General Post-hoc Contrasts
Using `emmeans` for pairwise comparisons of predicted means from complex linear, generalized linear, or mixed models:
```R
library(emmeans)
marginal = emmeans(model, ~ TreatmentGroup)
# Pairwise comparisons with Tukey adjustment
pairs(marginal, adjust="tukey")

# Compact Letter Display (CLD)
library(multcomp)
cld(marginal, Letters=letters)
```
