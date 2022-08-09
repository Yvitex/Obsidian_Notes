---
aliases: [np.sort(), np.argsort()]
---
# Sorting Arrays
[[Numpy Module]]'s way of sorting arrays withut using compelx [[Algorithm]]

We have this array called random:
![[Pasted image 20220728083624.png]]


```python
np.sort(random)
```
![[Pasted image 20220728083713.png]]

It will automatically sort the array per bracket. We could also find the indexes it will be arranged using `np.argsort()`
```python
np.argsort(random)
```

![[Pasted image 20220728083834.png]]

This will contain the indexes of the thing in the future sorting. Like for example, index 4 in the first part is 1 in the real set, index 2 is 2, index 3 is 2 again, index 0 is 4, index 1 is 6.
Combining it, will be \[1, 2, 2, 4, 6]


