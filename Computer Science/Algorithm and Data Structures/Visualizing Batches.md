# Visualizing Batches
To show an image from tensors, we use the [[Matplotlib module]] called  [[Showing Image in Matplotlib|imshow()]]. We also plot it into [[Subplots or Multiple Plots]] in a for loop

```python
def show_image(image, label, size=24):
	"""
	Plot the image and label using matplotlib
	"""
	plt.figure(figsize=[15, 10])

	for i in range(size):
		ax = plt.subplot(5, 5, i + 1)
		plt.title(unique_breeds[label[i].argmax()])
		plt.imshow(image[i])
```

If you are wondering what the hell is in the `plt.title()` simply we are getting all the unique breeds and getting the labels maximum index. 

Labels are composed of true and false arrays and because true is the highest value, then it will compare to the unique values resulting to `unique_breeds[15]` for example if the true value is located index 15. 

If we [[Extracting Batches|extracted batches]] we could use them for this
```python
show_image(training_img, training_label)
```
![[Pasted image 20220807112615.png]]



