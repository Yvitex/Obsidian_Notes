---
aliases: [crosstab(), groupby()]
---

# Comparing Data
Another way that [[Pandas]] are good at. The easiest way is by [[Creating a Plot using Pandas]]
But first we must learn how we could compare datas raw.
![[Pasted image 20220726113842.png]]

The first method is called `crosstab()`
```python
import pandas as pd

pd.crosstab(dataframe["Make"], dataframe["Colour"])
```

![[Pasted image 20220726170126.png]]

What this will do will regroup similar values into one and plot the frequency or occurence of the second attribute. Like for example, Honda have 2 blue cars and 1 red. Though because of the setup, we could do 2 separate [[Dataframe (Pandas)|dataframe]] interact inside it

The second method we may use is called `groupby()` method.
```python
import pandas as pd

dataframe.groupby(["Make"]).mean()
```
![[Pasted image 20220726170440.png]]

This will group similar values in the chosen attribute into one thing then recalculate all values in the column to its mean. For example, there are 4 toyotas in the [[Dataframe (Pandas)|dataframe]], it will be combined into one and all integer will be combined to its mean or average value

