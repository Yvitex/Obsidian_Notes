---
aliases: [.tick_params()]
---
# Customize the ticks
We could customize the plot ticks of [[Matplotlib module]] using `tick_params()`

```python
fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=dataframe["age"]
					 y=dataframe["chol"]
					 c=dataframe["target"])

ax.tick_params(color="white", labelcolor="white")
```

![[Pasted image 20220729083635.png]]


## Params
- color = color of the ticks
- labelcolor = color of the text in the tick