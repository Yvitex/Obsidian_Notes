---
aliases: [cross_val_score()]
---
# K-fold Precision Validation
Is a more advance metrics greater than [[Score Accuracy Measure|score()]] method. 
```python
from sklearn.model_selection import cross_val_score
```

This will accept 3 parameters which is the  [[Choosing a Model|chosen model]] , the X features [[Dataframe (Pandas)|dataframe]] and y [[Target]] dataframe in raw version unsplit

```python
X = heart_dis.drop("target", axis=1)
y = heart_dis["target"]

from sklearn.model_selection import train_test_split
np.random.seed(42)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

from sklearn.ensemble import RandomForestClassifier
model = RandomForestClassifier()
model.fit(X_train, y_train)

cross_val_score(model, X, y) # the use.
```

![[Pasted image 20220731182151.png]]

This will return 5 values, why? currently we are at 5-fold precision meaning, we are dividing the X and y dataset by 5 or 20% each. We are testing the 20% data, the rest is trainign and automatically fit and measure the score of each iteration where if the first part of the dataset is the [[Test Sets]], the next test sets would be the one next to it and the past test sets would become the [[Training Sets]]![[Pasted image 20220731182507.png]]

We could find the definition of [[Precision]] here. 

A key to note is that k-fold or cross validation is used in both [[Regression Machine Learning]] and [[Classification Machine Learning]] model and we could set each metrics scoring based on our need using the parameter `scoring`

## Classification
Scoring: [[Accuracy]], [[Recall]], [[F1 Score]]
Accuracy is the default scoring argument
```python
np.random.seed(42)
from sklearn.model_selection import cross_val_score
print(f"{np.mean(cross_val_score(model, X, y)) * 100:.2f}%")
```

Is the same as 
```python
np.random.seed(42)
cv_ac = cross_val_score(model, X, y, scoring="accuracy")
print(f"Accuracy Mean: {np.mean(cv_ac) * 100:.2f}%")
```

![[Pasted image 20220802083823.png]]

Recall:
```python
cv_ac = cross_val_score(model, X, y, scoring="recall")
print(f"Recall Mean: {np.mean(cv_ac) * 100:.2f}%")
```
![[Pasted image 20220802083848.png]]

F1:
```python
cv_ac = cross_val_score(model, X, y, scoring="f1")
print(f"F1 Mean: {np.mean(cv_ac) * 100:.2f}%")
```
![[Pasted image 20220802083911.png]]


## Regression
This will have scorign argument of [[R_Squared]], [[Mean Squared Error]], [[Mean Absolute Error]] in negative form. 

R^2 is the default, we do not need to include the scoring parameter
```python
cv_r2 = cross_val_score(model, X, y, scoring="r2")
print(cv_r2)
print(f"R2 mean: {np.mean(cv_r2) * 100:.2f}%")
```

![[Pasted image 20220802084111.png]]

Oh no!! This is too low!!

Negative Mean Absolute error:
```python
cv_r2 = cross_val_score(model, X, y, scoring="neg_mean_absolute_error")
print(cv_r2)
print(f"Negative MAE mean: {np.mean(cv_r2):.2f}")
```
![[Pasted image 20220802084438.png]]

Negative MAE is just a negative form of [[Mean Absolute Error]] where teh closer they are to 0, they more accurate it is amd as we could see, it is not accurate at all.

Negative Mean Squared Error:
```python
cv_r2 = cross_val_score(model, X, y, scoring="neg_mean_squared_error")
print(cv_r2)
print(f"Negative MSE mean: {np.mean(cv_r2):.2f}")
```

![[Pasted image 20220802084520.png]]



## Params
- X : the full original [[Exploring the Data (Methodology)|feature]] collection in [[Dataframe (Pandas)|dataframe]]
- y : the full [[Target]] unsplit actual data
- scoring: scoring method like MSE, MAE, R_Squared, Recall, Accuracy, F1