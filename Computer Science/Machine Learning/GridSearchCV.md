---
aliases: [GridSearchCV()]
---
# Grid Search CV
It is very simar to [[RandomSearchCV]] only that this is more a  brute force that it will try all combination in the grid parameter

```python
grid_2 = {
    "n_estimators": [100, 200, 500],
    "max_depth": [10, 20],
    "max_features": ["auto"],
    "min_samples_split": [4],
    "min_samples_leaf": [4, 6]
}
```

You may want to reduce the possivble combination because it will take longer and will burn your [[Processor|cpu]]. In our case, we have 3 x 2 x 1 x 1 x 2 x 5 = 60 possivle combination. Times 5 because we are tying to cross validate it by 5 or [[K-fold Precision Validation| 5 fold precision validation]]

```python
from sklearn.ensemble impor RandomForestClassifier
model = RandomForestClassifier(n_jobs=1)

gsc = GridSearchCV(estimator = model, 
				   param_grid = grid_2, 
				   cv = 5, 
				   verbose=2)
				   
gsc.fit(X_train, y_test)
```

We could get the best parameters using this
```python
gsc.best_params_
```
![[Pasted image 20220802162512.png]]

Check the [[(DM)Evaluation]] methods specially the [[Classification Report]] using [[Validation Sets]]
```python
y_predicted = gsc.predict(X_valid)

classif_anal(y_valid, y_predicted)
```
![[Pasted image 20220802162745.png]]
