# Manipulating Data
A way to manipulate our [[Dataframe (Pandas)|dataframe]] in [[Pandas]] is to override its variable. For example
![[Pasted image 20220726113842.png]]

If we want to lower case all string values in the Make [[(DM)Feature|feature]]
```python
dataframe["Make"] = dataframe["Make"].str.lower()
```

When we call again this [[Dataframe (Pandas)|dataframe]] The output is:
![[Pasted image 20220726180632.png]]

