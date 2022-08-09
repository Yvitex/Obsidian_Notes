---
aliases: [np.dot()]
---
# Dot Product
A way for us to calculate a [[Dot Product]] from 2 different arrays. This is used on [[Machine Learning]] to find some patterns in data in [[Numpy Module]]

```python
import numpy as np 

array1 = np.random.randint(10, size=(2, 3))
array2 = np.random.randint(10, size=(2, 3))

np.dot(array1, array2)
```
![[Pasted image 20220728055537.png]]

It will cause an error, why? because it is not alligned. [[Dot Product]] multiples the rows to the columns.
The inner value of an array which is 3 and 2 is not equal and should be (3, 2) and (2, 3) in which 2 == 2. To transform this, we could [[Transpose Numpy|transpose]] this  to  allign.  
```python
np.dot(array1.T, array2)
```
![[Pasted image 20220728055847.png]]


## Exercise
A good exercise is to replicate this table
![[Pasted image 20220728073914.png]]

using [[Numpy Module]] and [[Pandas]] and calculate the total using `np.dot()` method. Believe me, they could be combined and it needs constant [[Numpy Reshaping]].

