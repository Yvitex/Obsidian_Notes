
# Creating New Columns
In [[Pandas]], there are many different ways we could insert columns. One way is to append a [[Series (Pandas)|series]] the other is to appen a [[Python List]]

## Series Way
```python
import pandas as pd

series = pd.Series([5, 5, 5, 5, 5])
dataframe["Seats"] = series
```
![[Pasted image 20220727044200.png]]

To a dataframe of length 10, missing values are treated as NaN. To fill this up, we could refer how on [[Dealing With Missing Values]] section. 

## Python List Way
For a [[Python List]]. Creating an array of length 5 appended to a [[Dataframe (Pandas)|dataframe]] with length 10 will cause an error.
![[Pasted image 20220727044424.png]]

We need to fill it completely.
```python
list = [7.2, 6.5, 8.3, 5.3, 6.4, 5.3, 7.3, 6.2, 7.2, 8.4]
dataframe["Feature"] = list
```

## Calculation Way
We could actually create a new column based on a calculation derived from the values of other column. 
```python
dataframe["Feature"] = dataframe["feature 1"] * dataframe["feature 2"]
print(dataframe)
```

![[Pasted image 20220727050156.png]]

## Singe Value
When we apply a single value, an integer, float. boolean or an object string, it will be applied to all columns
```python
dataframe["Wheels"] = 4
```

![[Pasted image 20220727050311.png]]

