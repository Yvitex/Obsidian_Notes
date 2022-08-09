# Plot Yeah
Plotting takes some simple steps. 

First is to create a training data set with data evolved from [[Data Transformation]] and with function such as [[Splitting the Training and Testing Dataset]]. Recently, we also determined that INDUS and AGE does not add any explanatory value with their [[P-Value]] and confiemd by [[Bayesian Information Criterion]] so we also drop it along with the target from the feature variable. 

```python
price = np.log(data["PRICE"])
features = data.drop(["PRICE", "INDUS", "AGE"], axis=1)
X_train, X_test, y_train, y_test = train_test_split(features, price, test_size=0.2, random_state=10)
```


Next is to fit this model for the regression like in the example at calculating [[P-Value]] using [[Statsmodel]]
```python
X_include_constant = sm.add_constant(X_train)
model = sm.OLS(y_train, X_include_constant)
result = model.fit()
```

We could get the predicted value using `.fittedvalues` syntax in result object. 
Using this we could now calculate the residuals by this formula stated in [[Residual Sum of Squares]]
$$res = y - \hat{y}$$
Therefore, in code:
```python
residual = y_train - result.fittedvalues
```

Which in shortcut is just simply using `.resid` syntax
```python
residual = result.resid
```

testing the correlation between the actual value to the hypothetical data:
```python
print(round(y_train.corr(result.fittedvalues), 2))
```
The [[Correlation]] between the two should be high. It must be. 

To plot the [[Linear Regression]], we apply first a [[Scatter Plot]] with the fittedvalue as the predictor.
```python
plt.figure(figsize=[14, 9])

plt.scatter(y_train, result.fittedvalues, alpha=0.5, s=150, color="purple")
plt.plot(y_train, y_train, color="red")
plt.xlabel("Actual Data $Y_i$", fontsize=20)
plt.ylabel("Predicted Values $\hat{Y_i}$", fontsize=20)
plt.title("Log Actual Data vs Log Predicted Values")
plt.show()
```
![[Pasted image 20220623170326.png]]

But as we could see, we are workign with a transformed PRICE data. We need to revert it back using [[Euler's Number]] we could use using [[Numpy Module]] in the syntax of `np.e`

```python
plt.figure(figsize=[14, 9])

plt.scatter(np.e**y_train, np.e**result.fittedvalues, alpha=0.5, s=150, color="purple")
plt.plot(np.e**y_train, np.e**y_train, color="red")
plt.xlabel("Actual Data $Y_i$", fontsize=20)
plt.ylabel("Predicted Values $\hat{Y_i}$", fontsize=20)
plt.title("Actual Data vs Predicted Values")
plt.show()
```
![[Pasted image 20220623170550.png]]

```ad-Attention
title: Outlier FOUND!!!
collapse: open
We could see some strange pattern forming at the end of the graph, what does this mean? Is it a sign of the END? The return of CHRIST?? HOLY COW!

```


