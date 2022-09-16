# Keras Compilation
Next is to compile it, compilation have 3 main components which is the loss, the optimizer and the metrics, 
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

	model.compile(
		loss = tf.keras.losses.CategoricalCrossentropy(),
		optimizer = tf.keras.optimizers.Adam(),
		metric = ["accuracy"]
	)

```

to compile the [[Machine Learning Algoritm|model]] what we will do is to include the 3 main components
- [[Keras Losses]]
- [[Keras Optimizer]]
- [[Keras Metric]]
