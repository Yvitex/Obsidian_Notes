# Subplots
A way to create [[Subplots or Multiple Plots]] using [[Pandas]]

To do this, we just need to enable the subplots property to true. Here we are using [[Histogram (Pd)]]
```python
import pandas as pd

dataframe.plot.hist(subplots=True, y=["age", "cp", "oldpeak"])
```

We pass what  [[(DM)Feature|feature]] we want to be printed in a list, and enable the subplots

![[Pasted image 20220729050002.png]]


Some of the graph is meaningless and doesn;t provide useful data.

