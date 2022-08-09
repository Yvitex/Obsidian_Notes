# Histogram
![[Pasted image 20220605154157.png]]

## How can we create a meaningful Histogram for RAD?
In the Boston information in [[Data Exploration]]. We can prin out data description using this code
```
from sklearn.datasets import load_boston

boston_dataset = load_boston()
print(boston_dataset["DESC"])
```
![[Pasted image 20220605153907.png]]

We can see that RAD actually means, an **index** of accessibility to radial highways. It is an index so it is a label that describes a [[Exploring the Data (Methodology)|feature]] . We can print out the data to confirm this but first, we need to make this data in a `pandas.series`

```
import pandas as pd

data = pd.DataFrame(column=boston_dataset.feature_names, data=boston_dataset.data)
print(data["RAD"])
```

![[Pasted image 20220606044351.png]]

We can see from the printed data that the values are filled with floating point whole numbers, which seems unnatural as real world datas are chaotic like pimples. 

We can check the frequency of each number present in the indexes. This will serve 2 purpose, check for the lowest and highest while cheking the number of occurence we could compare to the histogram

```
print(data["RAD"].value_counts())
```
![[Pasted image 20220606044837.png]]

Basically, indexes represents the accessibility where 1.0 is the lowest accessibility, 24.0 has the highest accessibility and we can see the concentration of accessibility heavy aroun 24, 5, and 4. Most houses have great accessibility to highways, still the difference is so diverge. Coding it to our histogram
```
plt.figure(figsize=[15, 10])
plt.hist(data["RAD"], ec="black", color="purple", bins=24)
plt.xlabel("Accessibility to Highway")
plt.ylabel("Number of Houses")
plt.show()
```

![[Pasted image 20220606045211.png]]

We already know that the indexes are from 1 to 24, so we can set or `bins=` property to 24. Understanding the feature helps us understand the whole picture of the histogram.

We can add space between using `rwidth=`

```
plt.hist(data["RAD"], ec="black", color="purple", bins=24, rwidth=0.7)
```
![[Pasted image 20220606053714.png]]

One thing you could notice is a Histogram is similar to a [[Histogram using a Bar Graph|Bar Graph]]

