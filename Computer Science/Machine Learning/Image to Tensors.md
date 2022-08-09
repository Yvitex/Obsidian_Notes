
# Image to Tensors
to convert an image or any [[Unstructured Data]] into tensors, the steps are as followed
- [[Reading file to Tensors]] 
- [[Decode Image to Tensors]]
- [[Normalizing Tensors]]
- [[Resizing Tensor Image]]

Read the file. Means to convert it to tensor strings. We could create a function that is reusable for our purpose
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

We might also want to involve the labels, i mean, combining the tensor image to its label might seem to be a good idea so create a fucntion for it
```python
def pair_process(image, label):

	tensor = preprocess_img(image)
	return tensor, tf.constant(label)
```

[[Numpy Array vs Tensors|tf.constant()]] is a way to convert any array collection into tensors. 

![[Pasted image 20220806162838.png]]


You might also like [[Numpy Array vs Tensors]]