# Strings to Data For ML
Strings are things that [[Machine Learning Algoritm]] doesn;t understand. Machine understand numbers and not raw information, if we tell a computer what a string is, they won't understand it. Instead. what they understands are numbers. specifically [[Binary]] numbers.

For example is we have this [[Dataframe (Pandas)|dataframe]]:
![[Pasted image 20220730081533.png]]

The make column and colour column is a string that the machine doesn't understand. Also They are categories and so is the door number that evne though it is a number, doesn't necessarily means that it will help our [[Machine Learning Algoritm|model]]

If we persist to train the [[Machine Learning Algoritm|model]] using this strings. Here we are using a [[Random Forest Regressor]]
```js
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

from sklearn.ensemble import RandomForestRegressor
regr = RandomForestRegressor()
regr.fit(X_train, y_train)
```

![[Pasted image 20220730082732.png]]

What we could do is to transform the strings into [[Binary]] values of 0 and 1 using the [[OneHotEncoder Method]] paired with [[Column Transformer]]

```python
from sklearn.preprocessing import OneHotEncoder
from sklearn.compose import ColumnTransformer
```

Create an array of values which is the columns of the [[Dataframe (Pandas)|dataframe]] you want to transform
```python
columns = ["Make", "Colour", "Doors"] # include Doors, because it is categorical
```

Next is to instantiate the encoder and apply it to the Transformer
```python
columns = ["Make", "Colour", "Doors"] 
one_hot = OneHotEncoder()
transformer = ColumnTransform([("one_hot", one_hot, columns)], remainder="passthrough")
```

What just happen is just we apply a string called one_hot because that is what we are using, then apply the one_hot object, next is the list of names to be transformed and for the remainder, we passthrough it or do not touch it. 
Next is to actually use it in a [[Dataframe (Pandas)|dataframe]] which is the [[Exploring the Data (Methodology)|feature]]
```python
X_transformed = transformer.fit_transform(X)
```

This will be in a [[Numpy Module|ndarrays]]. Save this into a [[Dataframe (Pandas)|dataframe]]
```python
X_transformed = pd.DataFrame(X_transformed)
```

Now, try to [[Fit the data to the model and make a prediction]]
```python
X_train, X_test, y_train, y_test = train_test_split(X_transformed, y, test_size=0.2)
regr.fit(X_train, y_train)
```

It will suceed.









