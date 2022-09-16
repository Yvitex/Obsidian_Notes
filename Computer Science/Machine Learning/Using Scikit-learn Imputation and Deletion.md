---
aliases: [SimpleImputer()]
---
# Scikit Learn Version
Much longer process but the most correct one i think. [[SciKitLearn]] Provide us with methods that will do the [[Get the Data Ready|Data preparation]] for us. The process would be $$Split X and y \rightarrow 3sets \rightarrow Impute/Delete \rightarrow Convert and Encode$$

The process would be to separate [[Exploring the Data (Methodology)|feature]] from the [[Target]].  [[Splitting the Training and Testing Dataset]]. [[Imputation or Deletion]] then [[Convert classification string values into Numerical Data]].

```python
car_sales_missing = pd.read_csv("car-sales-extended-missing-data.csv")
car_sales_missing.head()
```
![[Pasted image 20220730171912.png]]

Some of this data is missing and we could check it using [[Null Value Detection]]. 
```python
car_sales_missing.isna().sum()
```
![[Pasted image 20220730172005.png]]

What we could do is to drop all rows that have missing [[Target]] values because they are useless using the [[Dealing With Missing Values|dropna()]]
```python
car_sales_missing.dropna(subset="Price", inplace=True)
car_sales_missing.isna().sum()
```
![[Pasted image 20220730172143.png]]

Here comes the splitting of data to input  X and output y
```python
X = car_sales_missing.drop("Price", axis=1)
y = car_sales_missing["Price"]
X.head()
```

![[Pasted image 20220730172244.png]]

The splittign the data again into [[Three Sets]] but probably only 2 which is [[Test Sets]] and [[Training Sets]]
```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
X_train.head()
```

![[Pasted image 20220730172422.png]]


Use the builtin importer of the [[SKLearn Module]], the `SimpleImputer` and also use the [[Column Transformer]] to transform the column
```python
from sklearn.impute import SimpleImputer
from sklearn.compose import ColumnTransformer

car_imput = SimpleImputer(strategy="constant", fill_value="missing")
door_imput = SimpleImputer(strategy = "constant", fill_value=4)
num_imput = SimpleImputer(strategy="mean")

car_feature = ["Make", "Colour"]
num_feature = ["Odometer (KM)"]
door_feature = ["Doors"]

transform_impute = ColumnTransformer([("car_imput", car_imput, car_feature), 
                                      ("num_imput", num_imput, num_feature), 
                                      ("door_imput", door_imput, door_feature)])

```

Next is to fit the values to the X_train and X_test [[Dataframe (Pandas)|dataframe]]
```python
X_train_filled = transform_impute.fit_transform(X_train)
X_test_filled = transform_impute.fit_transform(X_test)
```

This will output a [[Numpy Module|ndarrays]]
![[Pasted image 20220730173538.png]]

Set it into a [[Dataframe (Pandas)|dataframe]] and name each columns accordingly. Remember that depending on the position of the array in the [[Column Transformer|ColumnTransformer()]] will determine the position of each columns.
```python
X_train_filled = pd.DataFrame(X_train_filled, columns=["Make", "Colour", "Odometer (KM)", "Doors"])

X_test_filled = pd.DataFrame(X_test_filled, columns=["Make", "Colour", "Odometer (KM)", "Doors"])
```

![[Pasted image 20220730173655.png]]

If it is all good and correct. time to [[Convert classification string values into Numerical Data]]
```python
from sklearn.preprocessing import OneHotEncoder
from sklearn.compose import ColumnTransformer

columns = ["Make", "Colour", "Doors"]
one_hot = OneHotEncoder()
transformer = ColumnTransformer([("one_hot", 
								  one_hot, 
								  columns)], 
								  remainder="passthrough")

X_train_transformed = transformer.fit_transform(X_train_filled)
X_test_transformed = transformer.fit_transform(X_test_filled)
```

If the output of one of the variable is saying this
![[Pasted image 20220730174319.png]]

Then we could call [[Column Transformer|toarrays()]] to conver this to [[Numpy Module|ndarrays]]. Use the data to inser in a [[Dataframe (Pandas)|dataframe]].
```python
X_train_transformed = pd.DataFrame(X_train_transformed.toarray())
X_test_transformed = pd.DataFrame(X_test_transformed.toarray())
X_train_transformed
```

![[Pasted image 20220730174707.png]]

Then we could continue to [[Fit the data to the model and make a prediction]]

## Params
- strategy="constant" : will fill missing values in a constant manner meaning that the value don't change
- strategy="mean" : will fill the missing values with the [[Mean]] of all existing values in the column
- fill_value : will determine what to input to the missing values if it is set to constant


