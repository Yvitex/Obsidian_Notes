# Selecting Data
## Loc and Iloc
Another capability of [[Pandas]].
We could do 2 basic things which are `loc` and `iloc`

![[Pasted image 20220726150204.png]]

```python
import pandas as pd

dataframe.loc[3]
```

![[Pasted image 20220726150131.png]]

This will output all information in a column with an index of 3. 
Another example is this:![[Pasted image 20220726151056.png]]

```python
animals.loc[3];
```

Will output:
![[Pasted image 20220726151342.png]]

The other method is called `iloc`
Here we have a series with jumbled indexes

```python
animals.iloc[3]
```

Will output:
![[Pasted image 20220726151207.png]]

This method will follow the actual index rather than the custom index we created. 
This is useful if we add some [[Python Slicing]]
```python
imported.iloc[:5]
```

Will print up to 5 items, or print from index 0 to 4 excluding 5. ![[Pasted image 20220726151532.png]]
Doing this instead will result to 
```python
imported.iloc[2:5]
```
![[Pasted image 20220726151627.png]]

Printing from index 2 to 4 excluding 5. But for 3 parameter slicing.
```python
imported.iloc[2:10:2]
```
![[Pasted image 20220726151754.png]]

Prints out index 2 to 9 excluding 10, while jumping 2 steps at a time.


## Bracket Notation
![[Pasted image 20220726113842.png]]

```python
imported["Colour"]
```
This will select all the values in the column
![[Pasted image 20220726152033.png]]

We could also do a conditional thing, where we print out the row if the column condition is satisfied. Refer to the [[Dataframe (Pandas)|dataframe]] parts if confused. If we want to print out only the color while cars, then
```python
imported[imported["Colour"] == "White"]
```
![[Pasted image 20220726152302.png]]

Or if we want Odometer range greater than 100000, then do this
```python
imported[imported["Odometer (KM)"] > 100000 ]
```
![[Pasted image 20220726152430.png]]

We could also select the column [[(DM)Feature|feature]] or categories by using
```python
print(imported.columns)
```

![[Pasted image 20220726152616.png]]
