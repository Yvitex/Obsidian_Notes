## How to extract element in a list?


```python
tis_list = ["first", "second", "third", "fourth", "fifth"]
```

tis_list is a list, and to extract specific parts, we could use the following:

```python
tis_list [1] == "second"

tis_list[1: 4] == ["second", "third", "fourth"]

tis_list[1: ] == ["second", "third", "fourth", "fifth"]

tis_list[: 1] == "first"

tis_list[-1] == "fifth"
```



## How to delete elements in a list?

 `tis_list = ["first", "second", "third", "fourth", "fifth"]


```python
tis_list.pop() == ["first", "second", "third", "fourth"] 

tis_list.pop(0) == ["second", "third", "fourth"]  # deletes the element at index 0 
```


Related: [[Python]]

#python
