---
aliases: [.next()]
---
# Next iterator
A [[Python]] syntax that returns a single element from an array and remove it.
```python
array = [1, 2, 3 ,4]
iterator = iter(array)

print(next(iterator)) # output 1
print(next(iterator)) # output 2
```

This will accepts an iterator therefore we covnert arrays into one.