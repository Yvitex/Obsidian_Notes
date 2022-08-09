---
aliases: [head(), tail()]
---
# Viewing 
This could be done using [[Pandas]]. 

We could do 2 thins. First is the `head()` method
```python
import pandas as pd

dataframe.head()
```

This will print out the first 5 rows by default. We could also pass parameter that will specify the number of rows.
```python
import pandas as pd

dataframe.head(7)
```
![[Pasted image 20220726145605.png]]


The other is the tail which is the same as the head but in the last items in the [[Dataframe (Pandas)|dataframe]] or [[Series (Pandas)|series]]

```python
dataframe.tail(2)
```
![[Pasted image 20220726145727.png]]


