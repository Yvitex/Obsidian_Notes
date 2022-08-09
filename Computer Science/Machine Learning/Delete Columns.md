---
aliases: [drop()]
---
# Delete Columns
Aside from [[Creating New Columns]]  in [[Pandas]] we could remove the entire column if we wish, notice the parts of a [[Dataframe (Pandas)|dataframe]]. To delete the entire column, we could use axis=1 for it

```python
dataframe.drop(["feature"], axis=1)
```

But also, we need to use [[Overriding Data]] or even just adding the `inplace` parameter into true
```python
dataframe = dataframe.drop(["feature"], axis=1)
```

From:
![[Pasted image 20220727050701.png]]

To:
![[Pasted image 20220727051106.png]]


