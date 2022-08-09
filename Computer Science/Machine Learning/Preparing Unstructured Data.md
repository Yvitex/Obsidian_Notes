## Preparing Unstructured Data
After checking the data, we need to find a way to store the images into a proper [[Data Structure]]. Images, I mean a file path where we could get images and the id is the filename of that images. We could test it out by using the [[IPython]] library for outputing images.
```python
from IPython.display import Image
Image("/content/drive/MyDrive/dog_identification/train/"+label["id"][1]+".jpg")
```

![[Pasted image 20220806111347.png]]

To store it into an array, we could use the [[Python List Comprehension]] Technique
```python
filename = ["/content/drive/MyDrive/dog_identification/train/" + image_name +".jpg" for image in label["id"]]
```

Now we could do the outputing images like this
```python
Image(filename[10])
```
![[Pasted image 20220806111716.png]]


We could confirm if it is complete by comparing the length of files in the training directory by using the [[OS module]]
```python
import os
if (len(os.list_dir("/content/drive/MyDrive/dog_identification/train)/") == len(filename)):
	print("Compatible")
else:
	print("Not compatible")
```
![[Pasted image 20220806112222.png]]