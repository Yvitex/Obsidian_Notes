---
aliases: [.set(), .set_title(), .set_xlabel(), .set_ylabel()]
---
# Label and Title
We could do this by using the `.set()` method and pass in the named parameter called `title`, and `ylabel` `xlabel`

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=[10, 10])
ax.set(title="Something", ylabel="y", xlabel="x")
```

We could also do this individually if we want to change the color
```python
fig, ax = plt.subplots(figsize=[10, 10])
ax.set_title("Cholesterol per Age")
```

This have a parameter called `fontdict`, this will accept dictionary that will customize the font color
```python
fig, ax = plt.subplots(figsize=[10, 10])
ax.set_title("Cholesterol per Age", {"color": "white", "fontsize": 20})
```

Labels also have this
```python
fig, ax = plt.subplots(figsize=[10, 10])
ax.set_title("Cholesterol per Age", {"color": "white", "fontsize": 20})
ax.set_xlabel("Age", {"color": "white", "fontsize": 15})
ax.set_xlabel("Cholesterol", {"color": "white", "fontsize": 15})
```

