# Linear Regression
We use [[SKLearn Module]] to do this [[Linear Regression]] model

## Codes
First, import, `LinearRegression()` class and instantiate
```
from sklean.linear_model import LinearRegression

regr = LinearRegression()
```

From the data from [[Splitting the Training and Testing Dataset]]. We could pass the trainign data to the `fit()` method
```
from sklean.linear_model import LinearRegression

regr = LinearRegression()
regr.fit(X_train, y_train)
```
Now, we can extract the intercept and coefficient

```
from sklean.linear_model import LinearRegression

regr = LinearRegression()
regr.fit(X_train, y_train)
print(f"Intercept: {regr.intercept_}")
```

Intercept: 36.53305138282439

In our formula in [[Multivariable Regression]], we only have 1 intercept or $\theta_0$ and multiple coefficient or $\theta_1$, so we need to print out the coefficient in a table, in fact, using [[Pandas]] module

```
from sklean.linear_model import LinearRegression

regr = LinearRegression()
regr.fit(X_train, y_train)
print(f"Intercept: {regr.intercept_}")

pd.DataFrame(data=regr.coef_, index=X_train.columns, columns=['Coefficient'])
```
`index=` will name our [[Exploring the Data (Methodology)|data points]] with the X_train variable in its columns. `columns=[]` will name our columns.


![[Pasted image 20220610044953.png]]


## Conclusion
As we could see, we could relate it to our previous [[Correlation]] models, when there is a [[Negative Correlation]], the coefficient will be negative, if there is a [[Positive Correlation]], then there is a possitive sign in the coefficient.  For example, Room number has a possitive correlation with price, therefore, the coefficient is positive 3.1.  Pollution is negatively correlated with price, therefore, NOX and PRICE has a negative Coefficient.


Also, we could see yhr [[Dummy Variable]] CHAS to have a positive correlation with price, and that should be also valid, i think?

## Accuracy
We could also see their [[R_Squared|accuracy]] with `regr.score()` method, this accepts 2 variable. 
```
print("Training r-squared: ", regr.score(X_train, y_train))
print("Testing r-squared: ", regr.score(X_test, y_test))
```

Output:

"Training r-squared: 0.750121534530608"
"Testing r-squared: 0.6709339839115628"

We could see that the testing r_squared have a lower score in our data. This is because our algorithm haven't seen it yet. 
Actually, in this part, we are already starting to [[Evaluate and Deployment|evaluate]] our data


```ad-Attention
title: Not Significant !!!
collapse: open
Although, we already calculated the coefficient for each features. We have no idea about which one of the feature is important or not. Keeping this in mind, we must calculate the [[P-Values]] for each feature 

```


