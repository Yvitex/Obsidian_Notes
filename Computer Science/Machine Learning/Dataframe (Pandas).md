---
aliases: [dataframe]
---
# DataFrame
Another one of the most fundamental type in [[Pandas]]. It is a 2 dimentional collection of data structured in a table like manner.

```python
import pandas as pd

name = pd.Series(["BMW", "Toyota", "Honda"])
colors = pd.Series(["Red", "Blue", "Yellow"])

dataframe = pd.DataFrame({"Brand": name, "Colors": color})
print(dataframe)
```

It could accept a Python Dictionary as a parameter, where key is a string and the value may be a list or a [[Series (Pandas)|series]].

This won't accept a single scalar value like this
```python
dataframe = pd.DataFrame({"Brand": 1, "Colors": 1})
print(dataframe)
```

It needs to be inside an array or just pass an index in form `[0]`
```python
dataframe = pd.DataFrame({"Brand": [1], "Colors": [1]})
print(dataframe) # or

dataframe = pd.DataFrame({"Brand": 1, "Colors": 1}, index=[0])
print(dataframe) 
```

We could also [[Import Data from CSV to Dataframe|import]] and [[Export Data from Dataframe to CSV]]

## Parts of DataFrame
Dataframe can be broken down into the following
![[4.1 pandas-anatomy-of-a-dataframe.png]]

[[(DM)Data]] is each element value in each column name, or we could call it [[Exploring the Data (Methodology)|feature]] too, Remember that column is the vertical group and the row is the horizontal group. 

- Columns = axis 1
- Row = axis 0

Indexes could be edited like in [[Series (Pandas)|series]]


