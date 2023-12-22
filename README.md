# Logit_model_2

This code is focused on fitting a logistic regression model to a dataset, evaluating the model's performance, and analyzing its predictions, including calculating various diagnostic measures, confusion matrices, and plotting an ROC curve.

### Reading Data from a CSV File:

- `Presion.Orig = read.csv("Presion_Orig.csv", header = T)`
- This command reads data from a CSV file named `Presion_Orig.csv` into a DataFrame called `Presion.Orig`. The `header = T` argument indicates that the first row of the CSV file contains column headers.

### Fitting a Generalized Linear Model (GLM):

- `Ajuste.Presion.Orig <- glm(Coronarios ~ Diastolica, data = Presion.Orig, family = binomial)`
- A GLM is fitted with `Coronarios` as the response variable and `Diastolica` as the explanatory variable. The `family = binomial` argument suggests that it's a logistic regression, likely because `Coronarios` is a binary outcome.

### Model Summary:

- `summary(Ajuste.Presion.Orig)`
- This command displays a summary of the fitted model, including coefficients, statistical significance, and other diagnostics.

### Fitted Values:

- `fitted.values(Ajuste.Presion.Orig)`
- This calculates the fitted values (predicted probabilities) from the model.

### Hosmer-Lemeshow Test:

- `hoslem.test(Presion.Orig$Coronarios, fitted.values(Ajuste.Presion.Orig))`
- The Hosmer-Lemeshow test is used to assess the goodness-of-fit of the model. It compares observed outcomes with predicted probabilities.

### Storing and Accessing Hosmer-Lemeshow Test Results:

- `Bondad.Hosmer.No.Agrup <- hoslem.test(Presion.Orig$Coronarios, fitted.values(Ajuste.Presion.Orig))`
- `Bondad.Hosmer.No.Agrup$observed`
- The results of the Hosmer-Lemeshow test are stored in `Bondad.Hosmer.No.Agrup`, and the observed values are accessed.

### Residual Analysis:

- Residuals are calculated for the model using different types (`pearson` and `deviance`). Residuals are differences between observed and predicted values and are key in diagnosing model fit.

### Influence Measures:

- `hatvalues(Ajuste.Presion.Orig)`, `rstandard(Ajuste.Presion.Orig, type = "pearson")`, `rstandard(Ajuste.Presion.Orig, type = "deviance")`, `cooks.distance(Ajuste.Presion.Orig)`
- These commands calculate various statistics to identify influential data points that might disproportionately affect the model's performance.

### Binary Classification Based on Predicted Probabilities:

- `Categoria.Pred <- ifelse(fitted.values(Ajuste.Presion.Orig) >= 0.5, 1, 0)`
- This creates a binary classification based on the model's predicted probabilities, using 0.5 as a threshold.

### Confusion Matrix:

- `table(Presion.Orig$Coronarios, Categoria.Pred)`
- The confusion matrix is created to compare actual values against predicted categories.

### Alternative Threshold for Classification:

- `Categoria.Pred.013 <- ifelse(fitted.values(Ajuste.Presion.Orig) >= 0.13, 1, 0)`
- An alternative classification is created using a different threshold (0.13).

### Alternative Confusion Matrix:

- `table(Presion.Orig$Coronarios, Categoria.Pred.013)`
- Another confusion matrix is created for the alternative classification.

### ROC Curve Analysis:

- `library(pROC)`
- `CurvaROC <- roc(Presion.Orig$Coronarios, fitted.values(Ajuste.Presion.Orig))`
- `plot(CurvaROC)`
- The `pROC` library is used to create and plot a Receiver Operating Characteristic (ROC) curve, which is a graphical representation of the diagnostic ability of a binary classifier system.

### Reformatting Data for Further Analysis:

- The last block of code (starting with `Datos.Orig.Explicativa <- c(...)`) seems to reformat the original data and the model's fitted values for additional analysis, possibly for a more detailed evaluation of the model's performance.
