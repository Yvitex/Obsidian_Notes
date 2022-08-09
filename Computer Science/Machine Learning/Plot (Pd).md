# Plot 
Or line plot, whatever you call it, is another ability of [[Pandas]]. After [[Selecting Data]], we could call the `.plot()` method to create a line plot.
```python
import pandas as pd

dataframe["attribute"].plot()
```

![[Pasted image 20220726171919.png]]

`plot()` method will extract the axes that we could use to customize the title and labels
```python
ax = dataframe["attribute"].plot()
ax.set_title("title")
ax.set_ylabel("y")
ax.set_xlabel("x")
```

