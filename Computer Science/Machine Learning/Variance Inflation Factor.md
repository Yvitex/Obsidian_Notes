---
aliases: [vif, v.i.f]
---

# Variance Inflation Factor
This is used to test for [[Multicollinearity]] where if $$VIF > 10$$ therefore is it a Multicollinearity but if it is $$VIF < 10$$
therefore it is not. 

## Mathematical Formula
First we adhere to the [[Linear Regression]] rules for multiple parameter. For each features is the yhat calculation of $$TAX = \alpha_0 + \alpha_1RM + \alpha_2NOX + \dots + \alpha_3LSTAT$$
Second is tp find the reciprocal of [[R_Squared]] 
$$V.I.F = \frac{1}{(1 - R_{TAX}^2)}$$
## In code
To test for VIF, the module we are using is [[Statsmodel]], 
```python
from statsmodels.stats.outliers_influence import variance_inflation_factor
```

VIF will accept 2 parameters. `exog` or where you will get the data from and `exog_idx` or what row number it is from the `exog`
```python
variance_inflation_factor(exog=X_include_constant, exog_idx=1)
```
In this example, we use the [[Dataframe (Pandas)|dataframe]] from calculating [[P-Value]] that has a constant. This will output to 1.7145250443932485

To calculate all the features, what we are going to do is to create a for loop. And with [[Pandas]] [[Dataframe (Pandas)|dataframe]], we could store the data cleanly to a table
```python
list_data = []

for index in range(14):
    list_data.append(variance_inflation_factor(exog=X_include_constant, exog_idx=index))
pd.DataFrame({"Coef": result.params,"VIF": list_data})
```
![[Pasted image 20220623062109.png]]

## Conclusion
Here, we could see that there are no multicollinear relations based on the VIF values. 

```ad-important
collapse: open
But take note that other people use 5 as their threshold

```

