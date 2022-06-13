# Histogram
A great way for data visualization during presentation but also a technique to [[Exploring the Data (Methodology)]] we have in [[Data Science WorkFlow (Core)|data science]]

Simply it is a bar graph that displays the frequency or the number of occurence per variable.

![[Pasted image 20220605153352.png]]


## How to?
In [[Matplotlib module]], we can use this `.hist()` syntax

```
import matplotlib.pyplot as plt

plt.hist(data["PRICE"])
plt.show()
```

Refer to the data from [[First Step of Data Exploration]]
![[Pasted image 20220605154157.png]]

This will output... 
![[Pasted image 20220605155539.png]]

We can add more arguments to our histogram

```
import matplotlib.pyplot as plt

plt.hist(data["PRICE"], bins=50, ec="black")
plt.ylabel("Number of Houses")
plt.xlabel("Prices")
plt.show()
```

![[Pasted image 20220605160028.png]]

- ec is a named argument for edge color
- bins is the number of bars in the graph


There is also an alternative way of creating a [[Seaborn Histogram|histogram]] using [[Seaborn Module]]

Continuation: [[Advanced Data Analysis Histogram]]

