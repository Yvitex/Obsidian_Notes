# Panda's Dataframe
Using the module, we could set each data and column names into a beautiful table by using DataFrame attribute.

![[Pasted image 20220605154503.png]]

In here, we set each data using boston's data attribute and the columns with each of their own names.  
  
Now, the data will look like this

![[Pasted image 20220605154513.png]]


## Setting DataFramw with modified Index
```
pd.DataFrame(data=values, index=X_data.columns, columns=[])
```
`X_data.columns` is an index

## Merging an array as a column in a dataframe
![[Pasted image 20220605154537.png]]

![[Pasted image 20220605154541.png]]


## Counting the number of element for each column
![[Pasted image 20220605154602.png]]

To print out only the first 5 indexes

![[Pasted image 20220605154613.png]]

To print out only the last 5 indexes

![[Pasted image 20220605154621.png]]


## Get the Average from the Table
```
data["RM"].describe()
```
![[Pasted image 20220606035747.png]]
```
data["RM"].[[Descriptive Statistics using Python|mean]]()
```
![[Pasted image 20220606035822.png]]

Note: This displays the **minimum, maximum, median(50%) and mean**

## Frequency of Values
```
data["RM"].value_counts()
```

## Extracting index
```
fr = data["RM"].value_counts()
print(fr.index)
```

## AXIS
```
y = data.drop('f', axis=1) # Removes the Column

x = data.drop('f', axis=0) # Removes the ROW
```



Related: [[Python Programming]]