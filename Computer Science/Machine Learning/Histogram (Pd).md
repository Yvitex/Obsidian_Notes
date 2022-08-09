# Histogram
To create a [[Matplotlib Histogram]] within [[Pandas]], we could simply call the column we want using bracket or dot notation, kindly refer to [[Selecting Data]] in pandas section then calling the `hist()` method
```python
import pandas as pd

dataframe["attributes"].hist()
```

![[Pasted image 20220726171724.png]]



we could also do it like this
```python
dataframe.plot.hist(y="Odometer (KM)", bins=10)
```

![[Pasted image 20220729043646.png]]

