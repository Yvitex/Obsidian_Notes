---
aliases: [reset_index()]
---
# Fixing Shuffle
When we [[Shuffe Rows in Pandas]], we may want to reverse it back again to its orifinal arrangement, we could do this using `reset_index()`

```python
dataframe.reset_index()
```

We need [[Overriding Data]] to save this or `inplace=True`. Also, we may want to add the parameter of `drop` that will erase its previous indexing
```python
dataframe.reset_index(drop=True, inplace=True)
```
![[Pasted image 20220727054724.png]]


