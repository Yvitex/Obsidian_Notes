---
aliases: [np.min(), np.max(), np.unique(), np.argmin(), np.argmax()]
---
# Unique Numbers
Given random variable: 
![[Pasted image 20220728083624.png]]

A way to basically extract numbers that are special in [[Numpy Module|ndarrays]]. Or not. 
```python
np.unique(random)
```
![[Pasted image 20220728085442.png]]

This basically extract all numbers without duplicates into a single array of [[Numpy Vector|vector]]
To get the maximum number:
```python
np.max(random)
```
![[Pasted image 20220728085548.png]]

To get the min:
```python
np.min(random)
```
![[Pasted image 20220728085617.png]]

We could also get the index of the minimum value, but we need the axis to do so, see the [[Numpy Matrix|matrix]] parts. Axis 0 is the column and axis 1 is the rows. 
```python
np.argmin(random, axis=0)
np.argmax(random, axis=1)
```
![[Pasted image 20220728085835.png]]


