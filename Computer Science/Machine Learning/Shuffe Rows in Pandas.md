---
aliases: [sample()]
---
# Shuffling Rows
We could shuffle rows in [[Pandas]] using the `sample(frac=)` method. `frac` property is the percentage of data to shuffle, where 1 is 100 %
```python
dataframe.sample(frac=1)
```

If we want to save it, we need to assign it to a variable or use [[Overriding Data]]
```python
shuff = dataframe.sample(frac=1)
```

![[Pasted image 20220727054108.png]]

```
shuff = dataframe.sample(frac=0.5)
```

![[Pasted image 20220727054159.png]]



