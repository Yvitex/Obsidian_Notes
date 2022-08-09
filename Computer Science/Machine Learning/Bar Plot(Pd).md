# Bar graph
We could create a [[Matplotlib Bar Graph]] directly to [[Pandas]] [[Dataframe (Pandas)|dataframe]]

We could call it like this
```python
import pandas as pd

dataframe.plot.bar(x="Make", y="Odometer (KM)")
```

![[Pasted image 20220729043256.png]]

The y argument will determine how tall the bar is and the x will determine the  number of bars. 
Alternatively we could create this like this
```python
dataframe.plot(x="Make", y="Odometer (KM)", kind="bar")
```


## Params
- color : accepts an array of colors
- X : the labels
- y : the height
- figsize : size of plot