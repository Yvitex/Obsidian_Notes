# Bar Graph
![[Pasted image 20220606045211.png]]

We can replicate this [[Matplotlib Histogram]] using bar graph

![[Pasted image 20220605154157.png]]

The histogram above is a data\["RAD"], [[Pandas]] [[Series (Pandas)|series]]. We can create a bar graph using this using `plt.bar()` method.

First is to set up the required parameters, we need to get the frequency of the items. We can use the `.value_count()` to get the frequency of each value

```
frequency = data["RAD"].value_counts()
```

We can extract the index of the frequency using `.index` property
```
frequency.index
```

To create the bar graph, use [[Matplotlib module]] of `plt.bar()` method, this accepts 2 parameter, first is the x-axis values and next is the height.
```
plt.bar(frequency.index, height=frequency)
```

![[Pasted image 20220606051915.png]]


Notice that this is very similar to the histogram in [[Advanced Data Analysis Histogram]]

