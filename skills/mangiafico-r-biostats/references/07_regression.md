# Correlation and Regression

Analyzes linear and non-linear associations between measurement variables.

## Correlation
*   **Pearson Correlation (Parametric):**
    ```R
    cor.test(Data$X, Data$Y, method="pearson")
    ```
*   **Spearman Rank Correlation (Non-parametric):**
    ```R
    cor.test(Data$X, Data$Y, method="spearman")
    ```

## Simple Linear Regression
Fits $Y = \beta_0 + \beta_1 X + \epsilon$.
```R
model = lm(Y ~ X, data=Data)
summary(model)

# Plot data and fit
plot(Y ~ X, data=Data)
abline(model, col="red")
```
Validate residuals:
```R
par(mfrow=c(1,2))
plot(fitted(model), residuals(model))
hist(residuals(model))
```

## Curvilinear (Polynomial) Regression
Adding polynomial terms.
```R
model = lm(Y ~ X + I(X^2), data=Data)
summary(model)
```

## Multiple Linear Regression
Multiple independent measurement variables.
```R
model = lm(Y ~ X1 + X2 + X3, data=Data)
summary(model)
```
Check multicollinearity using Variance Inflation Factors:
```R
library(car)
vif(model)
```
