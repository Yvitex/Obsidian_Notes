---
aliases: [BIC]
---
# Should we Remove the High P-valued Features?
We could test the model using bayesian Information Criterion. The main principle is *"The Lower, the Better"*

IF model 1 is lower than model 2, therefore, model 1 is better.
![[Pasted image 20220623113057.png]]

## In code
Here, what we will use in calculating both the [[R_Squared]] and Bayesian Information Criterion, both inficating the truthfulness of data is the [[Statsmodel]]

```python
import statsmodels as sm
```

For an instance we already calculated the `fit()` of a [[P-Value]] model. We could use the fit to conceive the result data. 
```python
X_include_constant = sm.add_constant(X_train)
model = sm.OLS(y_train, X_include_constant)
result = model.fit()

org_coef = pd.DataFrame({'coef': result.params, 'P-Values': round(result.pvalues, 3)}) # for later use
```

Then to calculate the BIC and [[R_Squared]] is by, ofcourse, reading the [documentation](https://www.statsmodels.org/dev/generated/statsmodels.regression.linear_model.RegressionResults.html). We could find the documentation by reading the mini-docs in jupyter by pressing shift + alt on result object. 
![[Pasted image 20220623112819.png]]

Here we will found that, this could cacluate the r_square and BIC though dot syntax `rsquared` and `bic`

```python
print(f"BIC: {result.bic}")
print(f"R-Squared: {result.rsquared}")
```

This will output:
BIC: -139.74997769478875
R-Squared: 0.7930234826697582

Now, because the [[P-Value]] of some features are greater than 0.05. Should we remove them?
![[Pasted image 20220623050254.png]]

If we remove the INDUS columns. What we need to do is to use `.drop()` syntax of [[Pandas]] dataframe
```python
X_include_constant = sm.add_constant(X_train)
X_include_constant = X_include_constant.drop(["INDUS"], axis=1)
model = sm.OLS(y_train, X_include_constant)
result = model.fit()

coef_without_indus = pd.DataFrame({'coef': result.params, 'P-Values': round(result.pvalues, 3)})

print(f"BIC: {result.bic}")
print(f"R-Squared: {result.rsquared}")
```

The output will be:
BIC: -145.14508855591163
R-Squared: 0.7927126289415163

We could see that the BIC is a lot lower than before tha r-squared didn't change too much. Now, if we remove age...

```python
X_include_constant = sm.add_constant(X_train)
X_include_constant = X_include_constant.drop(["INDUS", "AGE"], axis=1)
model = sm.OLS(y_train, X_include_constant)
result = model.fit()

coef_reduced = pd.DataFrame({'coef': result.params, 'P-Values': round(result.pvalues, 3)})

print(f"BIC: {result.bic}")
print(f"R-Squared: {result.rsquared}")
```

The output will be:
BIC: -149.49934294224656
R-Squared: 0.7918657661852815

Now, it is a lot lower than before. We do not remove "CHAS" as it is only an index that adds some explanatory value. 

if we compare the P_values and Coef using [[Pandas]] dataframe

```python
frame = [org_coef, coef_without_indus, coef_reduced]
pd.concat(frame, axis=1)
```

![[Pasted image 20220623115909.png]]


```ad-question
title: Why do we do this?
collapse: open
Not because they have high P-value, it doesn't mean that it doesn't add anything to the model. Some features may add some explanatory data that will explain some things to the model.
```


