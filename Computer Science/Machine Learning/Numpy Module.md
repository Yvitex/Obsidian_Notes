---
aliases: [ndarrays]
---
# NUMPY 
Why numpy? It is a module that is under the hood optimization is written actually in [[C Programming Language]] which is faster than [[Python]], this is needed for faster calculation and also in [[Machine Learning]], we always wanted to use [[Binary]] values rather than actual numbers. 

This is a good alternative rather than using [[Python List]]. Instead of List, we are using Arrays. And also Numpy mean numerical python which is the backbone of python data science.

Why it is fast can be explained in the concept of [[Vectorization]] that is implemented via [[Broadcasting]]

It is very important to remember that all Numpy arrays are all type ndarrays

## Set-up
```
import numpy as np
```

### Example
  ![[Pasted image 20220605141433.png]]
  
The shape of this variable is (2, 2) where the first number is the number of rows and the second is the number of column.  
Using a method called `.reshape()`, we could modify the shape into something else.  
  
  ![[Pasted image 20220605141441.png]]
  
But it can't when the array shape is already been reshaped from the start.  
  
## Printing the columns  
  
To Print the columns, the syntax to use is variable \[:, 0] , where 0 is the column index you want to be printed.  

![[Pasted image 20220605141451.png]]

## Transpose Method and 2d Arrays
  
![[Pasted image 20220605142703.png]]


We can convert this variable to the shape of 7 rows and 1 column by adding  another \[] inside the array params. This will convert this into the shape of (1, 7) and to invert this number, we use `transpose()` method::: (7, 1)  
  
![[Pasted image 20220605142716.png]]
Another way of doing is through the `reshape()` method.  
  
![[Pasted image 20220605142724.png]]


## Natural Logarithm For DataSeries or DatFrame
```
np.log(dataseries)
```


## Euler Number
```python
np.e
```


Related: [[Python]]
  