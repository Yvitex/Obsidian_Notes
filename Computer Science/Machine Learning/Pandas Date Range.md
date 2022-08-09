---
aliases: [pd.date_range()]
---
# Date Range
Is a method in [[Pandas]] that will generate sequential dates useful in creating indexes. 

```python
import pandas as pd

dataframe["Dates"] = pd.date_range("1/1/2022", periods=10)
```

Periods is the amount of date to be generated and the string is the starting point, this will form a [[Series (Pandas)|series]] that will be inputed to the [[Dataframe (Pandas)|dataframe]]

![[Pasted image 20220729035057.png]]

