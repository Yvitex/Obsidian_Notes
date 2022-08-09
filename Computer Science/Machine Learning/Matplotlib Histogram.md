---
aliases: [ax.hist()]
---
# Histogram
In [[Matplotlib module]], we could create a histogram similar to a [[Matplotlib Bar Graph]]. 
```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
ax.hist(np.random.randn(1000))
```
![[Pasted image 20220728153111.png]]


We use a [[Normal Distribution]]  [[Generating Random Arrays|random number array]]

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

Refer to the data from [[Data Exploration]]
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

What we are finding inside a histrogram is what we call a [[Normal Distribution]] and adjust the bins accordingly until this curve appears.
There is also an alternative way of creating a [[Seaborn Histogram|histogram]] using [[Seaborn Module]]

Continuation: [[Advanced Data Analysis Histogram]]

