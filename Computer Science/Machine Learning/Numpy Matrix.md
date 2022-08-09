---
aliases: [matrix]
---
# Numpy Matrix
Another [[Numpy Module|ndarrays]] type of data composed of multiple dimensions from 2d to more than 2d

```python
import numpy as np

array2 = np.array([[1, 2, 3],
				   [4, 5, 6]])
```

![[Pasted image 20220727105633.png]]

Its anatomy looks like this
![[Pasted image 20220727110639.png]]

There are 2 rows and 3 columns. the [[Shape of Numpy|shape property]] should be (2, 3), 

It coul be more than 2 dimensions, for example this 3d array
```python
array3 = np.array([[[1, 2, 3],
				    [4, 5, 6],
				    [7, 8, 9]],
				    
				   [[10, 11, 12],
				    [13, 14, 15],
				    [16, 17, 18]]])
```

![[Pasted image 20220727105950.png]]


It is now composed of 2 sets, 3 rows and 3 columns, the [[Shape of Numpy|shape property]] shall be (2, 3, 3)
![[Pasted image 20220727110909.png]]

So the z axis is axis 0, the y axis is 1, and x to 2?


One way to understand the axis and number of dimension is [[Generating Random Arrays]] in 4 dimensions
```python
four_d = np.random.randint(0, 10, size=(2, 3, 4, 5))
```

![[Pasted image 20220727124203.png]]

The last of size is the column, the second to the last is the rows, the third to the last is the cluster enclosed by 2 consecutive brackets, and the first is the whole cluster separation enclosed by 3 consecutive brackets, 

Perform a slice operation to understand it more. 
```python
four_d[:, :, :, :4]
```

Will slice every 4 elements in the first row of every array.  Adding value to the next to the last will allow it to slice some columns, adding value to the next of the second last will slice the 3 arrays enclosed by 2 consecutive brackets and so on. 