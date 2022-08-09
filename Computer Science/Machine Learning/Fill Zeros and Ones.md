---
aliases: [zeros(), ones()]
---
# Zeros and Ones
Ability of the [[Numpy Module]] to create an arrayfilled by zeroes or ones in any [[Shape of Numpy|shape property]]

The one method will take a [[Shape of Numpy|shape property]] in tuple form.
```python
import numpy as np

ones = np.ones((2, 3))
```

![[Pasted image 20220727114240.png]]

This will return a float. But we could change it using [[Element Types|dtype property]]
```python
ones = np.ones((2, 3), dtype="int")
```

Just like `ones`, `zeros` will do the same thing but only it will output zeros. 
```python
zeros = np.zeros((3, 3), dtype="int")
```
![[Pasted image 20220727114722.png]]

