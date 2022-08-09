# CMAP
is a color range built in inside [[Matplotlib module]] that could be customized inside [[Scatter Plot]] or any other plots we could think of. The documentation tutorial and the list of available cmap could be found [here](https://matplotlib.org/stable/tutorials/colors/colormaps.html)

![[Pasted image 20220729113230.png]]

Here is an example from [[Scatter Plot]]

```python
plt.style.use("seaborn")

fig, ax = plt.subplots(figsize=[10, 6])
scatter = ax.scatter(x=over_50["age"],
                     y=over_50["chol"],
                     c=over_50["target"],
                     cmap = "winter")
```

cmap is set to winter.
![[Pasted image 20220729113634.png]]