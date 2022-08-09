---
aliases: [reshape()]
---
# Reshaping
One of the most complex topic i encountered in [[Numpy Module]] is the method of [[Broadcasting]] in performing [[Numpy Arithmetic]]. Basically we cannot perform an operation between arrays that have diverging [[Shape of Numpy|shape property]]. They need to be a match. 

For shape with (2, 3) to be multiplied by shape (2, 3, 3). It needs to be reshaped so that the following dimension is a match. for example, transform (2, 3) to (2, 3, 1) that matches to (2, 3, 3). The first 2 shapes matched the shape of the other and 1 simplified the column numbers into a singular value to each array. We could also do, transform (2, 3, 3) to (3, 2, 3). The trailing dimension match the dimension of (2, 3) which means it is a match. 

Here are more examples:
(6, 5, 1, 1) matches (6, 5, 4, 5)
(6, 5, 4, 1) matches (6, 5, 4, 5)
(4, 5) matches (6, 5, 4, 5)
(5, 4, 5) matches (6, 5, 4, 5)
(6, 5, 4, 5) matches (6, 5, 4, 5)

To reshape. Use this method
```python
array2.reshape(2, 3, 1)
```

