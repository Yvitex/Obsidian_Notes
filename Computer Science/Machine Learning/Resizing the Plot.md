---
aliases: [figsize=[]]
---
# Resizing the Plot
We could simply use the `figsize=[]` attribute that takes in an array and pass it as a parameter of [[Creating Data and Plot|plt.subplots()]]

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots(figsize=[10, 10])
```

The first parameter is the width and the second is the height