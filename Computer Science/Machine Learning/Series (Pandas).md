---
aliases: [series]
---
# Series
One of the most basic structure of [[Pandas]] module. It is a single dimentional collection of data composed of a single column.
```python
import pandas as pd

series = pd.Series(["BMW", "Toyota", "Honda"])
```
![[Pasted image 20220726112537.png]]

It acceps a [[Python List]]
We could also modify the indexes using the list
```python
import pandas as pd

animals = pd.Series(["dog", "cat", "elephant", "fox", "giraffe"], index=[0, 3, 2, 3, 19])
print(animals)
```
![[Pasted image 20220726145853.png]]



