# Batch Processing
After we convert [[Image to Tensors]]. We must convert them into batches, what it means is that we separate the each items into groups before training or testing the data. Why? Because to prevent the processor in being toast or to save time. Acoording to people, the best number of data is 32 size batches.

The first method to take is to [[Convert Tensors to Dataset]].
The second is to use the function of converting [[Image to Tensors]] to each dataset, If it is the [[Test Sets]], use this function
```python
IMG_SIZE = 244

def preprocess_img(image, size=244):

  """
  This function will convert image filepath into numerical tensors
  """
  
  # Read the file
  read_file = tf.io.read_file(image)
  # Convert into tensors with 3 channels
  tensor_img = tf.image.decode_jpeg(read_file, channels=3)
  # Normalize the image
  normalized = tf.image.convert_image_dtype(tensor_img, tf.float32)
  # Resize the image
  resized_img = tf.image.resize(normalized, size=[size, size])
  return resized_img
```

if it is the [[Validation Sets]] and [[Training Sets]] that have labels, use this function
```python
def pair_process(image, label):

	tensor = preprocess_img(image)
	return tensor, label
```

If it is a [[Training Sets]], we must shuffle it before using that above function, we could do it through [[Shuffling Data in Tensorflow|.shuffle()]] method. 

After wards, we could now batch it with size of 32 items using `.batch()` method
To make things simpler and reusable, make a function
```python
def batch_processing(X, y, batch_size=32, test_set=False, validation_set=True):
	"""
	Transform image filepath into batched tensors
	"""
	# Test Sets (No label)
	if test_set:
		data = tf.data.Dataset.from_tensor_slice((tf.constant(X)))
		data_batch = data.map(preprocess_img).batch(batch_size)
		return data_batch


	# Validation Sets (No shuffle)
	elif valiation_set:
		data = tf.data.Dataset.from_tensor_slice((tf.constant(X), tf.constant(y)))
		data_batch = data.map(pair_process).batch(batch_size)
		return data_batch

	# Training sets
	else:
		data = tf.data.Dataset.from_tensor_slice((tf.constant(X), tf.constant(y)))
		data_sh = data.shuffle(buffer_size=len(X))
		data_batch = data_sh.map(pair_process).batch(batch_size)
		return data_batch
```



## Params
- size : size of batch