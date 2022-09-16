---
aliases: [.as_numpy_iterator()]
---
# Extracting Batches
We could extract batches for perhaps for the purpsose  [[Visualizing Batches]] or others and we could do this through the help of [[Next Iterator]] method combined with `.as_numpy_iterator()`

This example returns a tuple of 2 values, one is a [[Exploring the Data (Methodology)|feature]] and the other is the [[Target]] or labels
```python
training_image, training_label = next(data.as_numpy_iterator())
```

If we do a 32 file [[Tensor Batch Processing]] then the length of these 2 must be
```python
len(training_img), len(training_label)
```

![[Pasted image 20220807110517.png]]

If we output the training_label, and it is a classification data, then it must contain an array of true and false
![[Pasted image 20220807110554.png]]


This will only return the first batch of data. To return all then we do this
```python
image_col = []
label_col = []

for image, label in data.unbatch().as_numpy_iterator()
	image_col.append(image)
	label_col.append(label)
```

