---
aliases: [plt.plot(), plt.subplots(), add_subplot(), add_axes()]
---
# Linear Plot
There are 3 ways we could generate a [[Matplotlib module]]'s plot figure. The third one is the recommended way of doing so. The normal way like `plt.plot()` is not so flexible

```python
x = [1, 2, 3]
y= [13, 17, 31]
```

## 1
In this method, we call the `add_subplot()`
```python
import matplotlib.pyplot as plt

fig = plt.figure()
ax = fig.add_subplot()
ax.plot(x, y)
```
![[Pasted image 20220728113739.png]]

## 2
This wil call the `add_axes` where we pass in an array that will determine how it will strech or size.
```python
fig = plt.figure()
ax = fig.add_axes([1, 1, 1, 1])
ax.plot(x, y)
```

![[Pasted image 20220728113959.png]]

## Recommended Way
Shortest way and the most flexible one that is based on Object Oriented Programming or [[OOP]], Here we call the `subplots()`
```python
fig, ax = plt.subplots()
ax.plot(x, y)
```

If you are confused about Ax and Fig, read the [[Anatomy of Matplotlib Plots]]



## Params
- x : the x value
- y : the y value
- label : reflected on the [[Adding some Legends|.legend()]]