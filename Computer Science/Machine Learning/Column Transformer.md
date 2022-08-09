---
aliases: [ColumnTransformer(), toarrays(), fit_transform()]
---
# Column Trasnformer
Use with [[OneHotEncoder Method|OneHotEncoder()]] to transform values in a column to a [[Binary]] data that is understandavke to a [[Machine Learning Algoritm]]

```python
from sklearn.compose import ColumnTransformer
transformer = ColumnTransformer([("name", object_encoder, ["columns"])])
tranformed_x = tranformer.fit_transform(X)
```

We could also use it to other methods that require column modification. For instance [[Using Scikit-learn Imputation and Deletion|SimpleImputer()]]
```python
from sklearn.imputer import SimpleImputer
from sklearn.compose import ColumnTransformer

columns_imputer = SimpleImputer(strategy="constant", fill_values="missing")
tranformer = ColumnTransformer([("columns_imputer", 
								 columns_imputer, 
								 ["something"])])
tranformed_x = tranformer.fit_transform(X) # written in ndarrays
```

Will return a [[Numpy Module|ndarrays]]

## Params
- A tuple with ("name", object, listOfColumns)
- remainder = passthrough = will set the rest of columns not included in the list to untouch

## Methods
- toarray() : sometimes, the final output of the fit_transform method is not [[Numpy Module|ndarrays]] but a compressed version, To transform this to ndarrays, use this