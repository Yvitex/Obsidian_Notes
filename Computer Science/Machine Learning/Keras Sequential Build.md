# Keras Sequential
We could build a model through keras module and we use a function in doing this
```python
def build_model(input_shape = INPUT_SHAPE, output_shape = OUTPUT_SHAPE, model = MODEL_URL):
	"""
	Build a model using Transfer Learning
	"""

	model = tf.keras.Sequential([
		tf.keras.layers.InputLayer(input_size=(224, 224, 3)),
		hub.KerasLayer(model),
		tf.keras.layers.Dense(units=output_shape, activation="softmax")
	])

```

`tf.keras.Sequential()` is one of the main model creation methods there is and it creates a sequential model. 
Sequential model will take an array and the content of the arrays are the layers of a [[Convolutional Neural Network]]. 

The first index item is the InputLayer, it is required to put this and this specify the size of the input using the [[Creating Input Layer Keras|tf.keras.layers.InputLayer()]]. 

The second item is the model that makes up the calculations using [[Creating Transfer Learning Layer Keras|hub.KerasLayer()]], and the next item is the output layer where we compress the result to a specific number of items, usually in a 224 by 224 with 3 channel picture, it will compress down resulting into a one dimensional array of values in a length of 1280.
![[Pasted image 20220807162728.png]]

If we only want 120 possible outputs, then we set the Dense units to 120, and because it is a [[Multiclass Classification]], then we activate it using "softmax"
So basically:

- [[Creating Input Layer Keras]]
- [[Creating Transfer Learning Layer Keras]]
- [[Creating Output Layer Keras]]

```ad-Notice
collapse: open
Notice that all of this method maybe dependent on the model used. In our case, MobilenetV2

```

The next thing to do is to do a [[Keras Compilation]]