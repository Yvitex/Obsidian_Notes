---
aliases: [tf.keras.Sequential()]
---
# Tensor Hub
This is the case where we could utilize [[Tensor Flow Hub]] rather than creating our own, this is called [[Transfer Learning]] where we utilize the [[Machine Learning Algoritm|model]] of other people rather than us creating it from scratch.

In our case, in dog classification problem, we are using [this model](https://tfhub.dev/google/imagenet/mobilenet_v2_130_224/classification/5)
We could also use [pytorch hub](https://pytorch.org/hub/) and [paperswithcode](https://paperswithcode.com/)

First , we need 3 things, the input shape, the output shape and the modeul url from [[Tensor Flow Hub]]
```python
INPUT_SHAPE = [None, 224, 224, 3]

OUTPUT_SHAPE = len(unique_breeds) # or simply 120

MODEL_URL = "https://tfhub.dev/google/imagenet/mobilenet_v2_130_224/classification/5""
```

To create a builder function for [[TensorFlow]], we do this 2 steps:
- [[Keras Sequential Build]]
- [[Keras Compilation]]

After we do this 2 steps, the final touch is indicating the input argument shape.
```python
model.build(INPUT_SHAPE)
```

The complete function is
```python
def build_model(input_shape=INPUT_SHAPE, output_shape=OUTPUT_SHAPE, model=MODEL_URL):
  print(f"Starting to build models using {model}")
  print(f"Output shape: {output_shape}")
  print(f"Input shape: {input_shape}")


  model = tf.keras.Sequential([
      tf.keras.layers.InputLayer(input_shape=(224,224,3)),
      hub.KerasLayer(model),
      tf.keras.layers.Dense(
          units=output_shape,
          activation="softmax"
      )
  ])

  model.compile(
      loss = tf.keras.losses.CategoricalCrossentropy(),
      optimizer = tf.keras.optimizers.Adam(),
      metrics = ["accuracy"]
  )

  model.build(input_shape)
  return model
```

To check whether it is working, use the [[Keras Summary]]
