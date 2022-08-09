---
aliases: [tf.fit()]
---
# Fitting the model
To fit the model in [[TensorFlow]], what we need first to do is to create a [[Keras Callback]] that will manage the training of our data and stop it when there is no improvement. This will save us more time than ever aside from doing some  [[Tensor Batch Processing]]

After defining the callbacks that we need, next step is to create a function that will use this callbacks and train or fit the data unto the model

```python
def train_model():
	"""
	Fit the data to the model and use the callbacks
	"""
```

First anf foremost, define an epoch, not the [[UNIX Time|epoch]] as in UNIX, but epoch as in the number of times the model will be trained to detect the patterns

```python
def train_model():
	"""
	Fit the data to the model and use the callbacks
	"""

	epoch = 100
```

The next step is to [[Choosing a Model in Tensor|create a model]] using sequentials. Create a function out of it and define it inside the train_model function

```python
def train_model():
	"""
	Fit the data to the model and use the callbacks
	"""
	epoch = 100
	model = create_model()
```

Next is to create a [[Keras Tensorboard Callback]]]. We already created a function so just execute it inside the function and also the [[Keras EarlyStopping Callback]]
```python
def train_model():
	"""
	Fit the data to the model and use the callbacks
	"""
	epoch = 100
	model = create_model()
	tensorboard = create_tensorboard()
	early_stopper = tf.keras.callbacks.EarlyStopping(monitor="val_accuracy", 
												 patience=3)


```

Now we could train the model using the `.fit()` function,
```python
def train_model():
	"""
	Fit the data to the model and use the callbacks
	"""
	epoch = 100
	model = create_model()
	tensorboard = create_tensorboard()
	early_stopper = tf.keras.callbacks.EarlyStopping(monitor="val_accuracy", 
												 patience=3)

	model.fit(x=training, 
			validation_data=validation, 
			epochs=epoch, 
			validation_freq=1, 
			callbacks=[tensorboard, early_stopper])
			
	return model
```

x will accept a tuple of (feature, target) sets. We don't need to define y anymore, training variable is a [[Tensor Batch Processing|batch processed]] variable with 32 size shape with (feature, target ) sets. 


![[Pasted image 20220808145508.png]]

as we could see the accuracy on the [[Training Sets]] is 1 or 100% which is a good thing and the accracy in the [[Validation Sets]] is only 0.6850. This is [[Overfitting]]
 Use the tensorboard to analyze what's going on
 ![[Pasted image 20220808150744.png]]

The[[Accuracy]] is increasing overtime, the training set overfits the data, the validation set did not. 
![[Pasted image 20220808150845.png]]

The loss is decreasing which is a good thing. But still it is [[Overfitting]]. The usual fix for this is by increasing the [[Training Sets]]

Now, we could also predict data
```python
valid_prediction = model.predict(validation, verbose=1)
```

This will output an array of values ![[Pasted image 20220808165420.png]]
And this values are in a length of 120 similar to the unique categories of breeds, these are arrays of possibilities, the highest value would be the most accurate prediction therefore we use [[Numpy Unique Numbers|np.argmax()]] to know it.

```python
print(unique_breeds[np.argmax(valid_prediction)])
```

The better way is this:
```python
index = 1
highest_argmax = np.argmax(valid_prediction[index])
highest_value = np.max(valid_prediction[index])
print(valid_prediction[index])
print(f"Summation : {np.sum(valid_prediction[index])}")
print(f"Maximum value : {highest_value}")
print(f"Index of the highest value : {highest_argmax}")
print(f"Label : {unique_breeds[highest_argmax]}")
```

![[Pasted image 20220808165801.png]]

The sum of all values must be near to 1. 

## Params
- x : accepts a tuple of (X, y) or features and target
- validation_data : sets the validation tuple of (X, y)
- epochs : sets how many times the we train the model
- validation_freq : sets how many times we will scan the validation per epochs
- callbacks : what are the callbacks we are going to use.



