---
aliases: [random.randint(), random.random(), random.rand()]
---
# Random arrays
We could do this using [[Numpy Module]]. Depending on the [[Shape of Numpy|shape property]] we provided will mold the [[Numpy Dimensions|dimension]] of that array

## 1
`random.randint()` will take the lowest minimum value inclusive and the highest value exclusive, and also the [[Shape of Numpy|shape property]] of that array
```python
import numpt as np

rand1 = np.random.randint(0, 10, size=(5, 5))
```
![[Pasted image 20220727115130.png]]


## 2
`random.random()` will generate random array values from 0 to 1 exclusive which are all float. 
```python
rand2 = np.random.random((5, 5))
```
![[Pasted image 20220727115257.png]]

## 3
`random.rand` is the same way but it accepts 2 parameter which is the row and the column, not a tuple.
```python
rand3 = np.random.rand(5, 5)
```

![[Pasted image 20220727115454.png]]

One thing to understand is that, this random number is not really random but Pseudo-Random numbers generated from a seed meaning if we manually set the [[Random Seed]], then the random numbers will be the same everywhere

## 4
This is a random [[Normal Distribution]]. [[Solidity 2 Main Function|normal function]]
```python
np.random.randn(10)
```

![[Pasted image 20220728154131.png]]

