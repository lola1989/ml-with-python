# CO2 Emissions Prediction Using OLS Regression

## Overview
Predict CO2 emissions using population and energy generation factors with an emphasis on **generalization, interpretability, and statistical rigor**.

This project demonstrates how classical linear regression can be used in a machine-learning pipeline to produce explainable environmental forecasts while maintaining strong out-of-sample performance.

## Data
- Source: Public CO2 and energy datasets (C02 emissions by state: https://www.eia.gov/environment/emissions/state/analysis/ and Electricity Data Browser: https://www.eia.gov/electricity/data/browser)
- Target: CO2 emissions
- Features: State net electricity energy generation and population

## Modeling Approach
- Ordinary Least Squares (OLS) Regression
- Hybrid workflow using statsmodels + scikit-learn
- Log transformation of skewed variables
- Feature selection via statistical significance (Wald tests)
- Assumption diagnostics and generalization testing

**Workflow:**
I used a hybrid inference-guided machine learning pipeline. I first performed an early train/test split to prevent data leakage. 
On the training data only, I fit an OLS regression model using statsmodels to conduct feature screening via Wald tests (p-values) 
and evaluate key assumptions. After selecting statistically relevant predictors, I rebuilt the training and testing matrices using 
only the retained features. I then refit the final model using scikit-learn, validated assumptions on the training residuals, 
and evaluated generalization performance on held-out test data.

This approach preserves model interpretability while ensuring out-of-sample reliability.

## Results
- R² (Test): 70.5%
- RMSE / MAE: 0.466/ 0.413
- Generalization: The model demonstrates stable predictive performance on unseen data with minimal overfitting.
- Interpretability: Coefficients remain directly interpretable, allowing clear insight into how energy and activity variables drive emissions.

## Key Takeaways
- Energy generation variables are the strongest drivers of CO2 output
- Log transformations significantly improved linearity and homoscedasticity
- Feature selection via statistical tests enhanced both interpretability and model stability
- The model is designed as an **explainable forecasting tool** rather than a black-box predictor, making it suitable for environmental analysis and policy-oriented decision support

## Documentation
- [Model Card](model_card.md)