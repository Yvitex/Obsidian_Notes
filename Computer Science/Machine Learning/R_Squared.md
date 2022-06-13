# The Goodness of Fit
$$R^2$$

Is a measurement of how much of a [[Linear Regression]] model can it explain on the real world. 

## Code
We could do this simply by using [[SKLearn Module]]'s `regr.score()`

```
from sklearn.linear_model import LinearRegression

regr = LinearRegression()
regr.fit(x, y)
regr.score(x, y)
```