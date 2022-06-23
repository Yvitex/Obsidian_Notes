---
alias: [p values, significance]
---
# P -Values
P-values indicates the amount of significance. To determine weather a certain [[Exploring the Data (Methodology)|feature]] is significant  or not, there are 2 things to consider

If $$P-Val < 0.05$$
Then it is *Significant*

If $$P-Val > 0.05$$
Therefore it is *Not Significant*

In [[Python Programming]], what module we're going to use is called [[Statsmodel]], this will calculate the p-values automatically as fast as 3 lines of code. 

## Coding
Import *statsmodel*
```python
import statsmodels.api as sm
```

Next is to get the X_train values, from [[Calculating Linear Regression using Training Dataset|training dataset]] and add a constant with it
```python
X_with_const = sm.add_constant(X_train)
```

After that is to get the OLS or [[Ordinary Least Squares Regression]] with y and x_with constant
```python
model = sm.OLS(y_train, X_with_const)
```

Next is to fit the model down. use the `var.params` and `var.pvalues` to get the necessary result
```python
result = model.fit()

print(result.params) # prints out the coefficients
print(result.pvalues) # prints out the significance
```

Though we could bettwe visualize this using [[Pandas]] dataframe. And also round the p-values to prevent its default format in significant notation
```python
import pandas as pd

pd.DataFrame({"Coef": result.params, "P_Values": round(result.pvalues, 3)})
```

![[Pasted image 20220623050254.png]]

## Conclusion
Here we could see that *Indus* and *Age* have p-values exceeding 0.05. Therefore they are deemed irrelevant. 
```ad-Notice
title: Now what?
collapse: closed
Should we remove it or not? To test the weather, if it is acceptable for these features to be removed, we could create a comparison model using BIC or [[Bayesian Information Criterion]]

```


#machineLearning

Related: [[Bayesian Information Criterion|BIC]]