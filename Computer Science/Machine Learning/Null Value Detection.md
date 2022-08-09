---
aliases: [.isna().sum()]
---
# Null Value Detectin In Dataframe
In a [[Dataframe (Pandas)|dataframe]] in [[Pandas]], we could detect the null values using `.isna()` method plus `.sum()`

```python
import pandas as pd

data = pd.read_csv("file.csv")
data.isna().sum()
```

![[Pasted image 20220730101052.png]]

So there are 50 missing values for each columns.