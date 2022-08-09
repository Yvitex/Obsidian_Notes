# Anatomy
![[4.1 matplotlib-anatomy-of-a-plot.png]]

We create the figure and the axes using this method in [[Creating Data and Plot]]
```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
```

Axes is the individual graph that lives inside the figure, figure is the parent component that house it all. 

The y labels and others could be set in the [[Customise the Plot]] section where we use the  [[Setting the Label and Title of the Plot|.set()]] method to do so.

