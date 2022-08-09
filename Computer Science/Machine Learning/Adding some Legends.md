---
aliases: [.legend(), .legend_elements()]
---
# Adding some legends
In [[Matplotlib module]], we could set this up using the `.legend()` method. Axes returns a value that could be transformed into legends
```python
fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=dataframe["age"]
					 y=dataframe["chol"]
					 c=dataframe["target"])
```

We could use the scatter variable to extract legends, it could be extracted by using the * signthen calling `.legend_elements()` and then choosing a title target.
```python
fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=dataframe["age"]
					 y=dataframe["chol"]
					 c=dataframe["target"])

ax.legend(*scatter.legend_elements(), title="target")
```

This would simply get the `dataframe.target.values` data.
![[Pasted image 20220729083635.png]]


When using the API style, it is bound to show automatically but if not, we could add this code
```python
ax.legend().set_visible(True)
```


## Params
- title =  the title of the label
