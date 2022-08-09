---
aliases: [imread()]
---
# Image to Arrays
This is a way to convert images into [[Numpy Module|ndarrays]] using [[Matplotlib module]]'s `imread()`
Importt he matplotlib's imread method found in the image module
```python
from matplotlib.image import imread
```

Simply get the filepath of the images and use the built in method to convert it.
```python
image1 = imread(fname="images/Lolu.jpg")
```

![[Pasted image 20220728092835.png]]

We could see that if we check for the type of the output.
```python
image1 = imread(fname="images/Lolu.jpg")
type(image1)
```

This will result into [[Numpy Module|ndarrays]]. So therefore. [[Matplotlib module]] and [[Numpy Module]] is connected.

Output the variable the result is:
![[Pasted image 20220728093027.png]]

And array that is equivalent to each pixels. JPG relies on PIL which is another library, and 


