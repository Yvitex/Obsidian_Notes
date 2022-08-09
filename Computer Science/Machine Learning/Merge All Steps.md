# Merge all steps
We could do this using [[SciKitLearn Pipelines]]

```python
from sklearn.model_selection import train_test_split, GridSearchCV

from sklearn.preprocessing import OneHotEncoder
from sklearn.compose import ColumnTransformer
from sklearn.impute import SimpleImputer
from sklearn.pipeline import Pipeline

from sklearn.ensemble import RandomForestRegressor
import pandas as pd

car_sales = pd.read_csv("car-sales-extended-missing-data.csv")
car_sales.dropna(subset=["Price"], inplace=True)

np.random.seed(42)

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

pipe_gridsearch = {
    "preprocessing__odometer__imputer__strategy": ["mean", "mean"],
    "model__n_estimators": [10, 1000],
    "model__max_depth": [None, 5],
    "model__min_samples_split": [2, 4],
    "model__max_features": ["auto"]
}

model = GridSearchCV(model, param_grid=pipe_gridsearch, cv=5, verbose=2)
model.fit(X_train, y_train)
model.score(X_test, y_test)
```

