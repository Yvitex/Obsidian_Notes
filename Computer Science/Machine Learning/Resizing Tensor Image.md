# Resizing Tensor Image
We do this because different Deep Learning Models needs different sizes of tensors. 

![[Pasted image 20220806155331.png]]

As we could see here, the sahpe is 1, 500 and we must transform it into square that is compatible with a prebuilt model, typically 244

```python
resized = tf.image.resize(tensor_channeled, size=[244, 244])
```

![[Pasted image 20220806155727.png]]
