---
aliases: [score()]
---
# Score Method
In [[SciKitLearn]], it is a method we could call after we [[Fit the data to the model and make a prediction]] in our [[Machine Learning Frameworks]]. 

```python
from sklearn.ensemble import RandomForestRegressor
reg = RandomForestRegressor()
reg.fit(X_train, y_train)
reg.score(X_test, y_test) //score method
```

![[Pasted image 20220731173109.png]]

It is the same as in [[Classification Machine Learning]].
![[Pasted image 20220731174940.png]]

What this would basically do is compare the predicted value or [[Y Hat]] and calculate how often the result is accurate in response to the total length of the elements. In a [[Binary Classification]] machine learning, it could be done like this
```python
y_train_array = np.array(y_test) // convert first from Series to ndarrays

count = 0
for i in range(len(y_preds)):
    if(y_preds[i] == y_train_array[i]):
        count += 1
        
count / len(y_preds)
```

![[Pasted image 20220731174951.png]]

I just count the numbers of similar values and divide it by the total numbers of element in an array.

Relying to only this measure is inefficient, the percentage value might only be an effect of luck from randomness, if this is your doubt, we could use [[K-fold Precision Validation]]



