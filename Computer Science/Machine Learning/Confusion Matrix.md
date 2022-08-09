---
aliases: [confusion_matrix()]
---
# Confusion Matrix
Is a technique we use in [[SciKitLearn]] to know in what part in the [[Classification Machine Learning]] model are the [[Machine Learning Algoritm|model]] getting confused

```python
from sklearn.metrics import confusion_matrix
```

Confusion matrix will take 2 parameters which is the actual value vs the predicted value

```python
y_preds = model.predict(X_test)
confusion_matrix(y_test, y_preds)
```
![[Pasted image 20220801120705.png]]

What the hell is this! You might ask, this is just the resulting [[True positive]], [[False positive]], [[True Negative ]] and [[False negative]]

We coudl visualize this by [[Plotting Confusion Matrix]]

![[Pasted image 20220801122743.png]]


In the anatomy above, the diagonal pattern is the correct [[True positive]] and [[True Negative]] values. We could see that most of them are correct compared tot he dark ones which the the false values. 

## Params
- actual value : the actual value of the [[Target]] created after split called y_test
- predicted value : the [[Y Hat]]. 