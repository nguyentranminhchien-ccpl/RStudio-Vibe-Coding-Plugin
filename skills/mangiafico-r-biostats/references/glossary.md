# Biostatistics & R Glossary

- **ANCOVA (Analysis of Covariance)**: Combines ANOVA and linear regression to compare group means while adjusting for a continuous covariate.
- **ANOVA (Analysis of Variance)**: A statistical model used to analyze the differences among group means in a sample.
- **Benjamini-Hochberg (BH)**: A procedure to control the false discovery rate (FDR) in multiple hypothesis testing.
- **Cate-Nelson Analysis**: A graphical and statistical technique used to partition bivariate data into two groups based on critical thresholds.
- **CLD (Compact Letter Display)**: Summarizes pairwise comparisons by assigning letters to groups; groups sharing a letter are not significantly different.
- **Cochran-Mantel-Haenszel (CMH) Test**: Evaluates the association between two nominal variables repeated across different groups or centers.
- **EMMeans (Estimated Marginal Means)**: Predicted means for a model, adjusted for other covariates. Essential for unbalanced designs.
- **Fisher's Exact Test**: An exact test used in contingency tables with small sample sizes where expected cell counts are < 5.
- **G-test of Goodness-of-Fit**: An alternative to the Chi-square test, preferred in biological sciences, using likelihood ratios.
- **Homoscedasticity**: The assumption that the variance of model residuals is constant across all levels of independent variables.
- **Interaction**: Occurs when the effect of one independent variable on the dependent variable changes depending on the level of another factor.
- **Kruskal-Wallis Test**: A non-parametric alternative to one-way ANOVA for comparing distributions of three or more independent groups.
- **McNemar's Test**: Tests for changes in paired nominal data (before vs. after comparisons).
- **Nagelkerke Pseudo R-squared**: A generalized R-squared measure used for logistic regression models.
- **Type I Sum of Squares**: Calculates factors sequentially in the order they are listed in the formula.
- **Type II Sum of Squares**: Calculates the effect of each factor after accounting for all other factors, preserving the principle of marginality.
- **Type III Sum of Squares**: Calculates the partial effect of each factor in the presence of all other factors. Requires configuring sum contrasts in R.
- **Welch's t-test**: An adaptation of the t-test for unequal variances. Default `t.test` implementation in R.
