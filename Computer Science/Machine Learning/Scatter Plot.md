---
aliases: [scatter()]
---
# Scatter Plot
A [[Matplotlib module]]'s plot that is composed of dots alligned in the x and y axis. We could call it after creating the figure by saying `scatter`

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
ax.scatter(x, np.exp(x))
```

X is created from [[Generating Range of Numbers|np.linspace()]] method that generates number from 0 to 10, 100 times. [[Numpy Arithmetic|np.exp()]] is the [[Exponential]] value of the number x.  ![[Pasted image 20220728144450.png]]

Using [[Numpy Trigonometric Functions]], we could do this
```python
fig, ax = plt.subplots()
ax.scatter(x, np.sin(x))
```

![[Pasted image 20220728145435.png]]



## Parameter
- x = x axis value
- y = y axis value
- c = scatter or dot color
- cmap = texture of the color, detil in [[Customize the CMAP]]

