# Data Transformation
One of the most popular data tranformation approach in [[Linear Regression]] is called **Log Transformation**

## Log Transformation
This helps reduce the [[Improving the model|skewness]] of [[Seaborn Histogram|Histogram]] and [[Linear Regression]] models. 

#### How does it work?
$$\ln(12) = 2.4849$$
$$\ln(50) = 3.9120$$
$\ln$ is called [[Natural Logarithm]] and note that it is different from the calculator's log. We could see that ln(12) and ln(50) are have low difference. So what? The point is, we could reduce the skewness by actually making each of the values close to each other. So that this graph: 
![[Pasted image 20220610150131.png]]

Could be fitted by the [[R_Squared]] or goodnes of fit like this

![[Pasted image 20220610150149.png]]


So by using this principle, we could turn this... Skeness of 1.11 to
![[Pasted image 20220610150434.png]]

To this, with skeness of -0.33, closer to a bell curve. 
![[Pasted image 20220610150504.png]]

## Code
The code to this is by simply using [[Numpy Module]]'s `np.log()` which accepts the [[Pandas]] dataframe or series as a parameter. 

```
import numpy as np

y_log  = np.log(data['PRICE'])
```

Next is to plot the data in the [[Seaborn Histogram]] using `sns.histplot()`

```
import numpy as np
import seaborn as sns

y_log  = np.log(data['PRICE'])
plt.figure(figsize=[13, 8])
plt.title(f"Skew Info: {y_log.skew()}")
sns.histplot(y_log, kde=True, bins=50)
plt.show()
```

How about in a [[Linear Regression]] with scatter plot in [[Seaborn Module]]

```
import seaborn as sns

sns.lmplot(x="LSTAT", y="PRICE", data=data, line_kws={"color": "red"},
			scatter={"s": 100, "alpha": 0.5})
```

![[Pasted image 20220610151321.png]]

Transforming this data using Logarithmic Transform. We input the same argument, but this time, the price must be in logarithmic form

```python
import seaborn as sns

tranformed_data = features # note that features is a variable of a dataframe data without Price columns
                             
transformed_data["PRICE_LOG"] = np.log(data["PRICE"])

sns.lmplot(x="LSTAT", y="PRICE_LOG", data=transformed_data, line_kws={"color": "red"},
			scatter={"s": 100, "alpha": 0.5})
```

Calculating the intercept and coefficient. We could modify the price into its log form before creating the training and test data split using `train_test_split()` from [[SKLearn Module]]

```
price_log = np.log(data["PRICE"])
features = data.drop("PRICE")

X_train, X_test, y_train, y_test = train_test_split(features, price_log, test_size=0.2, random_state= 10)

regr= LinearRegression()
regr.fit(X_train, X_test)

print(f"Intercept: {regr.intercept_}")
print("Train r-squared",regr.score(X_train, y_train))
print("test r-squared", regr.score(X_test, y_test))
pd.DataFrame(data=regr.coef_, index=X_train.columns, columns=['COEF'])
```

![[Pasted image 20220610160228.png]]


reversing back the coefficient, we use eulers number. The formula would be $$e^n$$
- n is the coefficient values in log form