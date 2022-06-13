# Sklearn
## Loading Sample Dataset
![[Pasted image 20220605153738.png]]
![[Pasted image 20220605153747.png]]
## Splitting Training and Testing data
```
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(features, target, test_size=0.2, random_state = 10)
```

## Linear Regression
```
from sklearn.linear_model import LinearRegression

regr = LinearRegression()
regr.fit(x, y)
print(regr.intercept_)
print(regr.coef_)

# Measure accuracy of prediction
print(regr.score(x, y))
```