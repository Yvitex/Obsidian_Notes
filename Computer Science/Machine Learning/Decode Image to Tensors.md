---
aliases: [tf.image.decode()]
---
# Decoding Images
[[TensorFlow]] have different methods for different image type, if our picture is in a jpeg format, then we could use this after we are done [[Reading file to Tensors]]

```python
tensor_img = tf.image.decode_jpeg(read_file, channels=3)
```

Because in a picture we are using red, green and blue, we could set the channels to 3 to make it colorful
![[Pasted image 20220806155045.png]]

Tensor images are like [[Images to Arrays]] using [[Matplotlib module]]

## Params
- contents : file that has been read to tensors
- channels : specify the amount of channels red green and blue