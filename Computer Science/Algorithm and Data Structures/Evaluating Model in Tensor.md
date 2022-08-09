# Evaluating Model
There are many ways we could do this, one is already done using [[Keras Tensorboard Callback]]
Another is through a function that compare the predicted value to the actual value or [[Accuracy]]
We could [[Extracting Batches]] from the original [[Validation Sets]] or the true values and compare it to the predicted values using [[Subplots or Multiple Plots]] nd [[Showing Image in Matplotlib|imshow()]]

```python
### Comparator function
def comparator (predicted_data, validation_data, index=0,):
	"""
	Compare between the Predicted and Validation Data
	"""
	valid_img_col = []
	valid_label_col = []
	for valid_img, valid_label in validation_data.unbatch().as_numpy_iterator():
	  valid_img_col.append(valid_img)
	  valid_label_col.append(valid_label)
	
	fig, (ax1, ax2) = plt.subplots(nrows=1, ncols=2, figsize=[10, 5])
	ax1.imshow(valid_img_col[index])
	ax1.set(title = f"{unique_breeds[np.argmax(predicted_data[index])]}({np.max(predicted_data[index]) * 100 :.2f}%)")
	ax2.imshow(valid_img_col[index])
	ax2.set(title = unique_breeds[np.argmax(valid_label_col[index])])
```

This will show this
![[Pasted image 20220808170115.png]]

A percentage of probability and the actual values. Aside from this, we could also make a bar graph that will compare the top 10 highest value 

```python
def bar_graph_comparator(index=0, validation_data=validation, prediction=valid_prediction):
	"""
	Bar graph comparing the validation and the top 10 prediction data
	"""
	# Top 10 indexes
	indexes = valid_prediction[index].argmax()[-10:][::-1]
	# Top 10 labels
	labels = unique_breeds[indexes]
	# Top values
	values = valid_prediction[index][indexes]
```

We could get the top 10 array by using [[Numpy Sorting Arrays|np.argsort()]] or sorting them the [[Python Slicing]] them. Next step is to get the true labels and the plotting the appropriate values.
```python
def bar_graph_comparator(index=0, validation_data=validation, prediction=valid_prediction):
	"""
	Bar graph comparing the validation and the top 10 prediction data
	"""
	# Top 10 indexes
	indexes = valid_prediction[index].argmax()[-10:][::-1]
	# Top 10 labels
	labels = unique_breeds[indexes]
	# Top values
	values = valid_prediction[index][indexes]

	# True value
	image_col = []
	label_col = []
	for img, label in validation_data.unbatch().as_numpy_iterator()
		image_col.append(img)
		label_col.append(label)

	bar_plot = plt.bar(np.arange(len(indexes)), values)
	plt.xticks(np.arange(len(indexes)), labels=labels, rotation="vertical")

```

We will use the x ticks instead to initialize the labels, because we need it rotated. 
```python
def bar_graph_comparator(index=0, validation_data=validation, prediction=valid_prediction):
	"""
	Bar graph comparing the validation and the top 10 prediction data
	"""
	# Top 10 indexes
	indexes = valid_prediction[index].argmax()[-10:][::-1]
	# Top 10 labels
	labels = unique_breeds[indexes]
	# Top values
	values = valid_prediction[index][indexes]
	# True value
	true_label = unique_breeds[valid_label_col[index]]

	image_col = []
	label_col = []
	for img, label in validation_data.unbatch().as_numpy_iterator()
		image_col.append(img)
		label_col.append(label)

	bar_plot = plt.bar(np.arange(len(indexes)), values)
	plt.xticks(np.arange(len(indexes)), labels=labels, rotation="vertical")

	if np.isin(true_label, values):
		bar_plot[np.argmax(true_label == values)].set_color("green")
	else:
		pass
```

![[Pasted image 20220809054539.png]]


We may want to arange this plots side by side and we could do this using [[Subplots or Multiple Plots]]
