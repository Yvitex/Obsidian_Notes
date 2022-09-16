---
aliases: [tf.save()]
---
# Saving the Model
We creates a function in doing so, to do this, we only need the file path and augmented as a parameter to the model's method `.save()`

```python
def save_model(model, suffix):

```

Suffix would be the ending part of the filename.  What we could do is to manipulate a string of path, and concatenate it with the [[Datetime]] module using the [[OS module]]

```python
def save_model(model, suffix):
	directory = os.path.join("/content/drive/MyDrive/dog_identification/models", 
							 datetime.now().strftime("%Y/%m/%d-%H:%M:%S"))

```

Add the suffixes and voila
```python
def save_model(model, suffix):
	directory = os.path.join("/content/drive/MyDrive/dog_identification/models", 
							 datetime.now().strftime("%Y/%m/%d-%H:%M:%S"))

	file_name = directory + "-" + suffix
```

Save it to the path
```python
def save_model(model, suffix):
	directory = os.path.join("/content/drive/MyDrive/dog_identification/models", 
							 datetime.now().strftime("%Y/%m/%d-%H:%M:%S"))

	file_name = directory + "-" + suffix
	print(f"Saving to {file_name}")
	model.save(file_name)
	return file_name
```

