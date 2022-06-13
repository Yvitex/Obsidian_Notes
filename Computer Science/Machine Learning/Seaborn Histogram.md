# Seaborn Histogram
Another wau of creating a histogram with additional features such as [[Probability Density Function]]

![[Pasted image 20220606033252.png]]

Probability density function is a line that travels through the different bars in the histogram. Simply it is a line that **estimates the distribution of the data**

## How to?
note: data comes from 

![[Pasted image 20220605154157.png]]

To create  a histogram, we use the `seaborn.histplot()` method.
```
import seaborn as sns
import matplotlib.pyplot as plt

sns.histplot(data["PRICE"])
plt.show()
```

[[Seaborn Module]] is highly based on [[Matplotlib module]]. We can modify this graph by adding some matplotlib features, for example...
```
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=[15,10])
sns.histplot(data["PRICE"])
plt.show()
```
This will output
![[Pasted image 20220606034127.png]]

To enable the [[Probability Density Function]], we can turn the `kde=` properties on.

```
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=[15,10])
sns.histplot(data["PRICE"], kde=True)
plt.show()
```
![[Pasted image 20220606034346.png]]

This histogram also has a` color=` and `bins=` feature.
![[Pasted image 20220606034439.png]]

## Conclusion
We can already, apparently see the average price a house has. The most frequenytly occuring count is usually the average, and based on this graph, we coul say that the average is between 20 - 25. To confirm this, we can find the [[Descriptive Statistics using Python|mean]] using our [[Pandas]] module

```
data["PRICE"].mean()
```