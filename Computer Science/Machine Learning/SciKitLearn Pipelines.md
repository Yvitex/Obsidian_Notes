---
aliases: [Pipeline()]
---
# Pipelines
Handles a series of steps available for [[Get the Data Ready|Data preparation]] or data transformation up to selecting [[Machine Learning Algoritm|estimator]]


Pipeliens could be used along with [[Column Transformer|ColumnTransformer()]] and [[OneHotEncoder Method|OneHotEncoder()]] and [[Using Scikit-learn Imputation and Deletion|SimpleImputer()]] side by side. one after another
We could create a transformer using a Pipeline
```python
features = ["Make", "Colour"]
feature_transformer = Pipeline(steps = [
	("imputer", SimpleImputer(strategy="constant", fill_values="missing")),
	("onehot", OneHotEncoder(handle_error="ignore"))
])
```

Then we could apply this transformer to the object column transformer
```python
transformation = ColumnTransformer([
	("text", feature_transformer, features),
	("doors", door_transformer, door_feature)
])
```



We could also use this to instantiate a model
```python
model = Pipeline(steps=[
	("transformation", transformation),
	("model", RandomForestRegressor())
])

mode.fit(X_train, y_train)
```


We could also use this pipeline models to tweak their [[Hyperparameter]]s and other parameters with [[GridSearchCV]].
One thing to remember abt this is that the names we inputed int he pipeline parameters is used to navigate to a certain parameter using a double underscore or \"\_\_"
So for example we have thid pipeline configurations
```python
text_cols = ["Make", "Colour"]
text_transformer = Pipeline(steps=[
    ("imputer", SimpleImputer(strategy="constant", fill_value="missing")),
    ("onehot", OneHotEncoder(handle_unknown="ignore"))
])

door_feature = ["Doors"]
door_transformer = Pipeline(steps = [
    ("imputer", SimpleImputer(strategy="constant", fill_value=4)),
    ("onehot", OneHotEncoder(handle_unknown="ignore"))
])

odometer_feature = ["Odometer (KM)"]
odometer_transformer = Pipeline(steps=[
    ("imputer", SimpleImputer(strategy="mean"))
])

transformation = ColumnTransformer([
    ("text", text_transformer, text_cols),
    ("door", door_transformer, door_feature),
    ("odometer", odometer_transformer, odometer_feature)
])

model = Pipeline(steps=[
    ("preprocessing", transformation),
    ("model", RandomForestRegressor())
])

X = car_sales.drop("Price", axis=1)
y = car_sales["Price"]

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2)
```

We could tweak them using [[GridSearchCV]] or event [[RandomSearchCV]]
```python
grid_pipline = {
	"preprocessing__odometer__imputer__strategy": ["mean", "median"], 
	"model__n_estimators": [10, 1000],
	"model__max_features": ["auto"],
	"model__min_samples_split": [2, 4],
	"model__max_depth": [None, 5]
}
```

The naming is basically means from processing > odometer > imputer > change parameter strategy
From Model >  change the arguments of n estimators.

Then apply this to [[GridSearchCV]]
```python
model = GridSearchCV(model, 
					 params_grid = grid_pipline, 
					 cv = 5, verbose = 2)

model.fit(X_train, y_train)
model.score(X_test, y_test)
```
![[Pasted image 20220803114157.png]]


## Params 
- steps : step by step scenario

