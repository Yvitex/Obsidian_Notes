---
aliases: [axhline()]
---
# Adding a dashline
We could add a horiontal dashline useful in visualizing the mean in a graph in  a[[Matplotlib module]]'s plot 

```python
fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=dataframe["age"]
					 y=dataframe["chol"]
					 c=dataframe["target"])
```

We could call it using the `.axhline()`
```python
fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=dataframe["age"]
					 y=dataframe["chol"]
					 c=dataframe["target"])

ax.axhline(y=dataframe["chol"].mean(), linestyle="--")
```


## Params
- y = y localtion of where to place the horizontal line
- linestyle = style of the line