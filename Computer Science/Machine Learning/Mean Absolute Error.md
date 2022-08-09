# Mean Absolute Error
$$MAE = \sum^n_{i=1}\frac{|\hat{y_i} - y_i|}{n}$$

[[Target|y-hat]] is the predicted value and y is the actual value.

[[SciKitLearn]] already have a method for it in metrics class
```python
from sklearn.metrics import mean_squared_error
mean_squared_error(y_test, y_predicted)
```

![[Pasted image 20220731171455.png]]

We oculd also manually code this us using [[Statistical Numpy Operation|np.mean()]] to the residuals
```python
result = abs(y_preds - y_test)
np.mean(result)
```

![[Pasted image 20220731171655.png]]


