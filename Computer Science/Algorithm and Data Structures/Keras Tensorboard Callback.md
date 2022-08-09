---
aliases: [tf.keras.callbacks.TensorBoard()]
---
# Keras Tensorboard Callback
In our case, the call back that we'll be using is an extension called TensorBoard, to import this, use this method in [[Google Colab]]
```python
%load_ext tensorboard
```

To use this, we need a directory where we will going to pass the results, we'll use a function in doing so.
```python
def create_tensorboard():
	logdir = os.path("/content/drive/MyDrive/dog_identification/logs")
```

we also add the time when we do this as a marker, therefore we use the join() keyword
```python
def create_tensorboard():
	logdir = os.path.join("/content/drive/MyDrive/dog_identification/logs"", 
							datetime.now().strftime("%Y/%m/%d-%H:%M:%S"))
```

Then we pass this to the tensorboard method
```python
def create_tensorboard():
	logdir = os.path.join("/content/drive/MyDrive/dog_identification/logs"", 
							datetime.now().strftime("%Y/%m/%d-%H:%M:%S"))
	return tf.keras.callbacks.TensorBoard(logdir)
```

To use this tensorboard, then we use this special method from [[Google Colab]]
```python
%tensorboard --logdir /content/drive/MyDrive/dog_identification/logs
```

We pass it the filename of where we are storing the logs.


## Params
- log_dir : directory to where to save the result