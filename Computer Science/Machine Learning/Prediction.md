---
aliases: [predict(), predict_proba()]
---
# Prediction
Is the final output of the [[Machine Learning Algoritm]], We could do this maybe in any [[Machine Learning Algoritm|model]]. 
```python
from sklearn.ensemble import RandomForestClassifier

clf = RandomforestClassifier()

X = data.drop("target", axis=1)
y = data["target"]

from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

clf.fit(X_train, y_train)
```

We could call a prediction by saying `.predict()` it will accept a [[Dataframe (Pandas)|dataframe]] int he same [[Shape of Numpy|shape property]] as the [[Training Sets]]. 

```python
clf.predict(X_test)
```

Comparing the predicted values to the actual values in X_test and y_test
![[Pasted image 20220731163231.png]]

80 percent of the time, we are correct in the prediction. 

In a classification prediction using [[Random Forest Classifier]], we could call the `predict_proba()` to see the percentage of accuracy for the classified values. 

```python
clf.predict_proba(X_test)
```

![[Pasted image 20220731163337.png]]

This is categorized by 0 and 1. In the first set of array, we have 89 percent change it would be 0 and 11 percent cchange it would be 1 so therefore it concludes that it must be 0 rather than 1. 

The predicted values that will be calculated is called [[Y Hat]]