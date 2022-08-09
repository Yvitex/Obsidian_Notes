---
aliases: [roc curve]
---
# Roc Curve
This [[(DM)Evaluation]] method will calculate a value from the [[True positive]] rate and [[False positive]] rate. [[SciKitLearn]] has a method to do this in the metrics class. This is a good evaluation method for [[Binary Classification]]

Because we are trying to get the [[False positive]] and [[True positive]], we need to get the true column probability of the [[Target]] using the [[Prediction|predict_proba()]]
```python
from sklearn.metrics import roc_curve

model.fit(X_train, y_train)
model.predict_proba(X_test)
```


Use the result as a parameter in contrast to the actual value
```python
model.fit(X_train, y_train)
y_proba = model.predict_proba(X_test)

roc_curve(y_test, y_proba)
```

Save the values to a variable, we only want the true column so we want to do a  [[Python Slicing]], this method will return a tuple with 3 different values or [[False positive]] rate or fpr, [[True positive]] rate or tpr and the threshold

```python
model.fit(X_train, y_train)
y_proba = model.predict_proba(X_test)
y_proba = y_proba[:, 1]

fpr, tpr, threshold = roc_curve(y_test, y_proba)
```

fpr and tpr will contain array of values which is quite useless but we could use it by [[Plotting ROC Curve]]

