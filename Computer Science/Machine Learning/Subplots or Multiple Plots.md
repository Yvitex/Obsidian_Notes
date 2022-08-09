# Multiple Plots
As we could see from the [[Anatomy of Matplotlib Plots]], we could create multiple axes in a single figure.
To do this, we set the axes into a tuple
```python
import matplotlib.pyplot as plt

fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(nrows=2, ncols=2, figsize=[10, 5])
```

The tuple axes is dependent on the number of rows and columns. Because we want 2 values in a row and 2 values in a column, we arrange the axes where axes 1 and 2 are together and 3 amnd 4 are together.

If we want 3 rows and  2 columns then we want to arrange the axes as:
((ax1,  ax2), (ax3, ax4), (ax5, ax6))

IF inverse, like 2 rows and 3 cols:
((ax1, ax2, ax3), (ax4, ax5, ax6))

We could not create some different plots like [[Creating Data and Plot|plt.plot()]], [[Matplotlib Histogram]], [[Scatter Plot]], [[Matplotlib Bar Graph]] using individual axes.
![[Pasted image 20220728155230.png]]


It could also be written like this
```python
fig, ax = plt.subplots(nrows=2, ncols=2, figsize=[10, 5])
ax[0,0].plot(np.random.random(100), np.random.random(100))
ax[0,1].scatter(np.random.random(100), np.random.random(100))
ax[1,0].bar(list(best_ln.keys()), list(best_ln.values()))
ax[1,1].hist(np.random.randn(1000), bins=100);
```

Here, we use only the index and treat it as if it is a 2d array



