---
aliases: [random.seed()]
---
# Random Seed
Basically sets the randomness static throughout. This is useful if we want to share the randomness we have on a chart. In [[Numpy Module]], we could freely or manually set the seed number into anything we want. 

THis principle basically proves that random number is not truly random but Pseudo random numbers. If we repeatedly executes the random function many times, then we will eventually see asimilar randombess from other random numbers as we finally have the same seed.

In short [[Generating Random Arrays]] is not random

```python
import numpy as np

np.random.seed(4)
rand4 = np.random.randint(0, 20, size=(5, 5))
rand4
```
![[Pasted image 20220727121751.png]]


```
np.random.seed(4)
rand5 = np.random.randint(0, 20, size=(5, 5))
rand5
```

![[Pasted image 20220727121805.png]]

