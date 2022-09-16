---
aliases: [tf.data.Dataset.from_tensor_slices()]
---
# Converting Tensor to Dataset
What this will do is compress tensors into Dataset. 
```python
data = tf.data.Dataset.from_tensor_slices(tf.constant(X))
```

This method will accept a tensor in which we could get by using [[Numpy Array vs Tensors|tf.constant()]] to the data array.

![[Pasted image 20220807101054.png]]

