# Broadcasting
An ability of the [[Numpy Module]] to perform arithmetic operation with diverging dimensions.

Here are some [information](https://numpy.org/doc/stable/user/basics.broadcasting.html) regading it

The basic principle is, the 2 [[Numpy Module|ndarrays]] are arithmetically calculatable if they are the same [[Shape of Numpy|shape property]] or one of them is 1. 

So for example we have a (2, 3, 3) array [[Shape of Numpy|shape property]], it is compatible with 2 dimensional array with (3, 3) shape. The trailing dimension should match, if it is 2 dimensional, then it must be the same or one of the shape is 1 or a single column


```python
array3 = np.array([[[1, 2, 3],
                    [4, 5, 6],
                    [7, 8, 9]],
                   
                   [[10, 11, 12],
                    [13, 14, 15],
                    [16, 17, 18]]])

array2 = np.array([[1,2,3], [4,5,6]])

array3 * array2
```

Will cause an error in [[Broadcasting]] as they have different [[Numpy Dimensions]]. What we could do is to [[Reshape]] it to concede the rules of [[Broadcasting]]
```python
array3 = array3.reshape(3, 2, 3)
```

this will still be equivalent to 18 in [[Element Size|size property]]. 
```python
array3 * array2
```

![[Pasted image 20220727162859.png]]


OR, the recommended way is to transform the column into 1. 
```python
array2 = array2.reshape(2, 3, 1)
array2 * array3
```

Notice that  the first dimenstion 2 and 3 matched the shape of array3, we just add 1 to make the column singular.
![[Pasted image 20220728050451.png]]

