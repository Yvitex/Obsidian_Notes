# Python Dictionary
The syntax is basically like Javascript Objects
```python
dict = {
	"key": "value"
}
```

Can be traversed using this method
```python
for key, values in dict.items():
	print(f"Key: {key}, Value: {values}")
```


It also have an ability to map to separate array data using the dict() keyword

```python
mapped = dict(zip(df.columns, [1,2,3,4,5,6]))
```

