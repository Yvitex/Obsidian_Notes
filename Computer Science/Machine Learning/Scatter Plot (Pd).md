# Scatter Plot for Pandas
Aside from normal [[Plot (Pd)]], we could create any kind of plots like [[Scatter Plot]] using the `kind` property. Scatter will not work for a [[Series (Pandas)|series]] but to a dataframe. It should have 2 values, x and y that will take the values from the [[(DM)Feature|feature]] column and compare it to one another.

![[Pasted image 20220726173045.png]]

```python
import pandas as pd

dataframe.plot(x="Odometer (KM)", y="Price", kind="scatter")
```

Or instead of inserting `kind` property, we could also create a direct method to do so.
```python
dataframe.plot.scatter(x="Odometer (KM)", y="Price")
```

![[Pasted image 20220729040723.png]]


The arguments above plot the odometer to the price. 

Although it is working, it will have less flexibility rather than using the actual way of creating [[Scatter Plot]] using [[Matplotlib module]]'s OOP. For example
![[Pasted image 20220729052029.png]]

In this example, we can't set the label properly. To create a flexible scatter plot, we do this,
```python
fig, ax = plt.subplots(figsize=[10, 5])
over_50.plot.scatter(x ="age",
                     y = "chol",
                     c = "target",
                     ax = ax)
```

We set the parameter ax to variable ax which means axes. 
![[Pasted image 20220729052411.png]]

Now, it looks the same but we could [[Customise the Plot]] to our own liking in any way we want.
```python
fig, ax = plt.subplots(figsize=[10, 5])
over_50.plot.scatter(x ="age",
                     y = "chol",
                     c = "target",
                     ax = ax)

ax.set_xlim([40, 100])
```

![[Pasted image 20220729052738.png]]

## Parameters
x = values in the x axis
y = values in the y axis
c = color of the scatter dots, can be used to color the dots or create a diverding colors base on different range of values like [[Binary]]
ax = accepts an axes of a fgure to adapt into it


Note that this is not the real proper way to create a plot... See [[Dataframe to Plots using OOP]]

