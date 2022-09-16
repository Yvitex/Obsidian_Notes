---
aliases: [summary()]
---
# Keras Summary
This will indicate teh trainable and non trainable parameters in a [[Transfer Learning]] model. To do this, we use the `.summary()` method to an instance of a [[Keras Sequential Build]].

```python
model.summary()
```

Rge first 3 lines are from a function [[Choosing a Model in Tensor]] section so don't mind it. 
![[Pasted image 20220808044728.png]]

The firs layer or the keras_layer is the original trained datas by the original creator of the model. The dense layer that have a shape indicatted in the [[Creating Output Layer Keras|tf.keras.layers.Dense()]] is the parameters indicated in our own shape model.