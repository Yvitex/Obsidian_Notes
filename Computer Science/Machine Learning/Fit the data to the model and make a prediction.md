---
aliases: [fit(), score()]
---
# Fitting the Data
After [[Pick a Model]], we fit the data using the model we choose. This one of the easiest part of [[Scikitlearn Workflow]]

```python
from sklearn.ensemble import RandomForestRegressor
reg = RandomForestRegressor()
reg.fit(X_train, y_train)
reg.score(X_test, y_test)
```

`.fit()` will work in detecting the patterns in a data and `.score` will work on testing the accuracy of that data.