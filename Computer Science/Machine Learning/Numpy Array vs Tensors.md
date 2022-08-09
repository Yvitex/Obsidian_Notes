---
aliases: [tf.constant()]
---
# Numpy Array vs Tensors
In an image, we convert first [[Images to Arrays]] using [[Matplotlib module]].
```python
from matplotlib.image import imread
np_image = imread(filename[0])
np_image
```

![[Pasted image 20220806131141.png]]

As we could see, a picture contains pixels and each pixels contain 3 values or red green and blue combination from 0 to 255. This is the same on how tensors would look.

Convert it into tensors using `tf.constant()`, it is away to convert an array of numbers into tensors.
```python
tensor_img = tf.constant(np_image)
tensor_img
```
![[Pasted image 20220806131329.png]]

