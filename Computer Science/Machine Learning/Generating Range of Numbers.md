---
aliases: [np.linspace(), np.arange()]
---
# Range of Numbers
We want to print out 0 to 9 in an array? [[Numpy Module]] have a quick fix for that. Use `arange()` method

```python
import numpy as np

range = np.arange(0, 10, 1)
```

The arguments are the starting number, the second is the last number but not included in the count, and lastly the step.

If we want to generate an array of numbers that is evenly spaced, we could use the `linspace()` method
```python
range = np.linspace(0, 100, 10)
```

The parameters is the start, the stop and the number of elements inside the array


