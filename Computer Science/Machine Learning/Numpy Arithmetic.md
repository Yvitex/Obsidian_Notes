---
aliases: [np.sum(), np.log(), np.exp(), np.cumsum()]
---
# Numpy Arithmetic
We already knew that [[Numpy Module]] utilizes [[Broadcasting]] operation to make the calculation fast. 

Testing it in the [[Jupyter]] notes: First is  generate random number using [[Generating Random Arrays|random.random()]]
```python
many_number = np.random.random(1000)
```

To time it, we will compare the sum() operation to the np.sum()
```python
%timeit sum(many_number)
%timeit np.sum(many_number)
```
![[Pasted image 20220727165407.png]]

For exampel we have this arrays of ones
![[Pasted image 20220727161744.png]]

And some 2 dimensional array
![[Pasted image 20220727161800.png]]


```python
import numpy as np

array2 + ones
```
![[Pasted image 20220727161829.png]]

Each number in the 2d array was added by the values of ones each. 
If we do this instead
```
rat = np.array[2, 3, 4]
array2 + rat
```

![[Pasted image 20220727162042.png]]

It is calculated like this, first value 1 + 2 = 3,  2 + 3 = 5, 3 + 4 = 7, 4 + 2 = 6.
We could also do division, multiplication and subtraction. We could also do this in a single value
```
array2 + 10
```
![[Pasted image 20220727162323.png]]

10 is added to all values in the array,

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

Other operations include summation
```python
np.sum(array2)
```

Other arithmetic expression includes [[Exponential]] and  [[Natural Logarithm]]
```python
np.exp(array2)
np.log(array2)
```

It is also important to know the [[Statistical Numpy Operation]]

