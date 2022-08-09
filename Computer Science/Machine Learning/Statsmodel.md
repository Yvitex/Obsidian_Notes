# StatsModels'

### Importing Statsmodel
```python
import statsmodels as sm
```
#### Adding constant
```python
X_include_constant = sm.add_constant(X_train)
```

#### Calculating P-Values
```python
X_include_constant = sm.add_constant(X_train)
model = sm.OLS(y_train, X_include_constant)
result = model.fit()

pd.DataFrame({'coef': result.params, 'P-Values': round(result.pvalues, 3)})
```
```ad-Notice
title: Pandas Detected
collapse: closed
We imported the values inside a [[Pandas]] [[Dataframe (Pandas)|dataframe]]

```

### Importing Variance Inflation Factor Calculator
[[Variance Inflation Factor]]
```python
from statsmodels.stats.outliers_influence import variance_inflation_factor
```

### Calculating VIF
```python
variance_inflation_factor(exog=X_include_constant, exog_idx=1)
```
