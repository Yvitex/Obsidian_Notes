# Picking the Right Model
Om [[SciKitLearn]]'s website, they already have a map that will guide you in choosing the right [[Machine Learning Algoritm|model]]
or [[Machine Learning Algoritm|estimator]]. Click [here](https://scikit-learn.org/stable/tutorial/machine_learning_map/index.html) to the website.

![[Pasted image 20220731113554.png]]

We need to start with the start and follow through the guide, if we are doing some classification then the selection is already mapped for us. We could click on each green boxes and it will redirect us to a certain webpage that will introduce on how to use it and what to import. 

In this example, we are [[Importing Toy Data Set]] of boston house price
```python
from sklearn.dataset import load_boston

boston = load_boston()
boston_df = pd.DataFrame(boston["data"], columns=boston["feature_names"])
boston_df["target"] = boston["target"]
```

If we search for the length of the [[Dataframe (Pandas)|dataframe]], it will output 506 rows. If we look at our map, we would fall into using [[Ridge Regression]]
```python
from sklearn.linear_model import Ridge
ridge = Ridge()
```

Bonus is [[Splitting the Training and Testing Dataset]] then ditting it to the model which is not the correct thing to do because we need to mind things like [[Multicollinearity]] but this is just to learn how to use the map.
```python
X = boston_df.drop("target", axis=1)
y = boston_df["target"]

from sklearn.model_selection import train_test_split

np.random.seed(42)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
ridge.fit(X_train, y_train)
ridge.score(X_test, y_test)
```

The best model to choose when working the [[Dataframe (Pandas)|dataframe]] is [[Random Forest]]
