---
aliases: [mean, median, midpoint]
---


# Descriptive Statistics
It is a statistics that summarize or describe a collection of data enabling us to analyze it at first glance

## 2 Important Parts
The 2 most important parts of Descriptive statistics is the mean and median. Sometimes they might have the same values but they are entirely different from each other

### Mean
[[Mean]] is the average of the values

##### Formula:
$$\frac{x_1 + x_2  + \dots+ x_n}{n}$$

### Median
Is the center point of the values or the middle value/ midpoint

##### Formula:
$$\frac{x_1 + x_n}{2}$$
- where $x_1$ is the lowest number
- where $x_n$ is the highest number


### Example Case
![[Pasted image 20220606105752.png]]

In this example, mean and median are both equal to each other. But usually, this is not the case because real world data are like pimples as I said on [[Advanced Data Analysis Histogram]]

Usually, datas look like this.
![[Pasted image 20220606053714.png]]

To calculate the mean and median, simply use the [[Pandas]] module `.describe()`, or if you just want a single set of data, then we can use these method: `.mean()` , `.median()`, `.max()`, `.min()`

```
import pandas as pd
print(data.describe())
```
![[Pasted image 20220606110247.png]]

Refer to [[Data Exploration]]
