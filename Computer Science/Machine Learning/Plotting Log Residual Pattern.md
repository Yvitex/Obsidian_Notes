# Residual Pattern
A continuation in [[Residual Pattern]] calculation
To do this, after [[Splitting the Training and Testing Dataset]] and [[Plotting Linear Regression for Model with Training Dataset]]
```python
price = np.log(data["PRICE"])
features = data.drop(["PRICE", "INDUS", "AGE"], axis=1)
X_train, X_test, y_train, y_test = train_test_split(features, price, test_size=0.2, random_state=10)

X_include_constant = sm.add_constant(X_train)
model = sm.OLS(y_train, X_include_constant)
result = model.fit()
```
We could get the the residual patter by creating a plot with the fitted values and the residuals. Use the [[Matplotlib module]] in this case
```python
plt.scatter(x=result.fittedvalues, y=result.resid, c="navy", alpha=0.6)
plt.title("Logarithmic Residual Vs Fitted Values")
plt.ylabel("Fitted Values")
plt.xlabel("Residuals")
```

![[Pasted image 20220725053154.png]]

We could see that our [[Scatter Plot]] is cloudy, but we must also not that this data is undergoed [[Data Transformation]], applied some [[Natural Logarithm]] stuff. 

We could check it further by making our residuals in a histogram using [[Seaborn Module]]
```python
sns.distplot(result.resid, color="navy")
plt.title("Log Residual P")
plt.title(f"Log Price Model: Resid")
```
![[Pasted image 20220725053659.png]]

We could see that it looks like a bell curve, it is because it is in logarithm. If we print out the mean and the skew of this residuals
```python
print(round(result.resid.mean(), 3))
print(round(result.resid.skew(), 3))
```

output: -0.0 which is the normal nature of the residuals and  0.118 which means it will look highly symmetrical. After this, we must create Plotting Normal Residual Pattern

## Conclusion
We could notice in this distribution that is is completely normal, but at some parts of the scatter we could see some allignment in the price. This might be because of some missing features or missing explanatory variables that will help us explain it, 
