# Saving Picture
We could save the plot using code in [[Matplotlib module]]. To do this, we just need to call the entire figure and call the method `savefig()`

```python
plt.style.use("seaborn")

fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=over_50["age"],
                     y=over_50["chol"],
                     c=over_50["target"],
                     cmap = "winter")
fig.savefig("data.png")
```

Or just do a right click then save, 

[[SciKitLearn]]

