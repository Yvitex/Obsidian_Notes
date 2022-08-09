---
aliases: [tf.image.convert_image_dtype]
---
# Normalization
Normalize means makign a range of values, like 1 to 331314213413 become only a range of number from 0 to 1. 

![[Pasted image 20220806155123.png]]

This value range from 0 to 255 but we could transform it into float using this
```python
normalized_image = tf.image.convert_image_dtype(tensor_image, tf.float32)
```

![[Pasted image 20220806155331.png]]


## Params
- image :  [[Decode Image to Tensors|decoded image to tensors]]
- dtype : type of transformation