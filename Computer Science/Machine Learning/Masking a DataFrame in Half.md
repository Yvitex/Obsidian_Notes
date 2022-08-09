# How to mask a DataFrame
Welcome back to the Hell Tutorial🙂💖
Today I will teach you how to create a mask for your [[Correlation]] data Frame.
But unlike your stupid school, or college or whatever that teaches you useless stuff.
Here, I will teach you a more sensibly useless stuff.


Suppose, you have this data frame from [[Correlation]] section

![[Pasted image 20220606123158.png]]


And you want to erase the **top** triangle of your data frame.
![[Pasted image 20220606123158 - Copy (2).png]]

What we're going to do is to first create a initial mask composed of composed of nothing but zero using the [[Numpy Module]] that has a similar [[Dataframe (Pandas)|dataframe]] structure  like our correlation table

```
import numpy as np

mask = np.zeros_like(data.corr())
```

mask will output a bunch of 0
![[Pasted image 20220606163742.png]]


Next is to extract the indices of the top triangle by using `np.triu_indices_from()`, this numpy method will accept the dummy correlation figure as an argument. 
```
import numpy as np

mask = np.zeros_like(data.corr())
triangle_indices = np.triu_indices_from(mask)
```

Next is to set the indices we get as true

```
import numpy as np

mask = np.zeros_like(data.corr())
triangle_indices = np.triu_indices_from(mask)
mask[triangle_indices] = True
```

Printing out the mask will output: 
![[Pasted image 20220606164116.png]]

Now this will be our mask to be applied in [[Correlation Matrix]]

