---
aliases: [np.mean(), np.std(), np.var()]
---
# Statistical Numpy
[[Numpy Module]] have their own method to calculate staistical datas.
We have this array as given:
![[Pasted image 20220727161800.png]]

We could fint he average or [[Mean]] using the `np.mean()`
```python
import numpy as np

np.mean(array2)
```
![[Pasted image 20220727170034.png]]

We could also find  [[Standard Deviation]] and [[Variance]] using the following
```python
np.std(array2)
np.var(array2)
```
![[Pasted image 20220727170221.png]]

[[Standard Deviation]] is only the squareroot of [[Variance]]. We could do this instead
```python
np.sqrt(np.var(array2))
```

![[Pasted image 20220727170350.png]]

So the basic concept is this.
If we have an array that is spreadout away from the mean, then there is a high variability
```python
high_var = np.array([1, 10, 100, 1000, 30000, 400000]) # high variability
low_var = np.array([2, 4, 6, 8, 10]) # low variability
```

In low var, the meaan is 6 which is near at 10 and 2 but in high_var, the mean is 71851.83333333333 which is far from 1 and 400000


