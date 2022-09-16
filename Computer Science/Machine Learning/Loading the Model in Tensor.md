# Loading the Model in Tensor
To load a model, is different if we are using [[Tensor Flow Hub]] models. If that's the case, we add a custom object property

```python
def load_model(path):
	
```

to load a model we simply need the file path as well as the custom object which is an object that has a key argument of `KerasLayer`, we'll pass it the [[Creating Transfer Learning Layer Keras|transfer learning layer]]

```python
def load_model(path):
	print(f"Loading model from {path}")
	model = tf.keras.models.load_model(path, custom_obj={"KerasLayer": hub.KerasLayer})
	return model
```

