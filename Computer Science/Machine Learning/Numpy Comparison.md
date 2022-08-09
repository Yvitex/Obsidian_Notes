# Comparison
[[Numpy Module]] also have its own comparison operators such as >, < >=, == . 

```python
import numpy as np

array1 = np.array([1, 2, 3])
array2 = np.array([[1, 2, 3],
			       [4, 5, 6]])

array1 > array2
```

![[Pasted image 20220728081141.png]]

To understand this, we know that 1 is not greater than 1, . and 1 is not greater than 4 so it is false. 2 is not greater than 2 and 2 is not greater than 5 and so on.

the array value in the first array is [[Broadcasting]] itself to each row of the second array.

We could also do comparison to singular value
```python
array2 == 2
```
![[Pasted image 20220728081522.png]]



