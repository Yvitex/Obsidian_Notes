---
aliases: [RandomizedSearchCV()]
---
# Random Search CV
A method is [[SciKitLearn]] that allow us to randomly select a parameter and filter the best combination we could have that could improve in iterations. IN here, we do not need to create some [[Validation Sets]] but the [[Splitting the Training and Testing Dataset]] is sufficient enough

[[Get the Data Ready]] and use a [[Random Seed]]
```python
X = heart_dis.drop("target", axis=1)
y = heart_dis["target"]

np.random.seed(42)

from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
```

Create a dictionary that will contain all [[Hyperparameter]] and an array of values that the program will randomly select.
```python
grid = {
    "n_estimators": [10, 100, 200, 500, 1000, 1200],
    "max_depth": [None, 5, 10, 20, 30],
    "max_features": ["auto", "sqrt"],
    "min_samples_split": [2, 4, 6],
    "min_samples_leaf": [1, 2, 4]
}
```

Initialize our [[Machine Learning Algoritm|model]]
```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(n_jobs=1) // will alter the processing power used
```

Import the random search cv
```python
from sklearn.model_selection import RandomizedSearchCV
```

THis will accept some parameters such as the [[Machine Learning Algoritm|model]] or estimator, the dictionary of values and [[Hyperparameter]] names,  [[K-fold Precision Validation|cross validation]] , number of iterations and verbose
```python
rsv = RandomizedSearchCV(estimator = model, 
						 param_distribution = grid, 
						 n_iter = 10 , 
						 cv = 5, 
						 verbose = 2)
```

[[Fit the data to the model and make a prediction|fit()]] the data using the Ramdomized Search CV object
```python
rsv.fit(X_train, y_train)
```
![[Pasted image 20220802151724.png]]

It should start the searching function

We could get the most accurate combination by getting the properties of `best_params_`
```python
rsv.best_params_
```
![[Pasted image 20220802151910.png]]

We could test it using the [[(DM)Evaluation]] methods from [[Classification Report]]

```python
y_valid_prediction = rsv.predict(X_valid)
classif_anal(y_valid, y_valid_prediction)
```

![[Pasted image 20220802152310.png]]

## Params
- estimator : the model you want to use
- param_distribution : the [[Hyperparameter]] and some values you want to use
- n_iter : how many combinations you want to try
- cv : a cross validation technique similar to [[K-fold Precision Validation]]
- verbose ; logging output related