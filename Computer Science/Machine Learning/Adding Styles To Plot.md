---
aliases: [style.available, style.use()]
---
# Adding Styles to Plot
[[Matplotlib module]] have builtin styles they would offer, to view the list of styles available, just type in
```python
import matplotlib.pyplot as plt

plt.style.available
```
![[Pasted image 20220729094520.png]]

To use this styles, we use the `use()` method, in this example, we use a [[Plot (Pd)]]
```python
plt.style.use("seaborn")
ax = dataframe["Price"].plot()
ax.set_title("Shhs")
ax.set_ylabel("Prices")
```
![[Pasted image 20220729094659.png]]

