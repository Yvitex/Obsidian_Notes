---
aliases: [dropna(), fillna()]
---
# Null data
[[Pandas]] One of the major problem in the initial [[Data analysis]] is the fact that in the real world, the data provided to us have some parts empty, so  when we use the [[Describe DataFrame|info()]] method and realized we have some missing data, we could either fill this null using `.fillna()`
or drop the entire row using `.dropna()`

Reak world data looks like this
![[Pasted image 20220726181032.png]]

The usual case is that we dropped all of this rows with NAN because it doesn't help us in anyway. But we also need somehow to have a copy of the original data so we do this
```python
dataframe_dropped_na = dataframe.dropna()
```
 
 When we output this:
![[Pasted image 20220726181316.png]]


If we want to override the orginal data, we could add the argument `inplace` to True.
```python
dataframe.dropna(inplace=True)
```

If want to fill in this data, we could use this method
```python
dataframe["Odometer"] = dataframe["Odometer"].fillna(0)
```

This will [[Overriding Data|manipulate data]] and replace all NAN in the Odometer column with 0
![[Pasted image 20220726181722.png]]

Alternatively we could do this instead of overriding
```python
dataframe["Odometer"].fillna(inplace=True)
```



