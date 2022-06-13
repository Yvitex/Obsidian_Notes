# Senseless Correlation
[[Correlations doesn't implicate causation.]] We already knew about this. To check wether our  [[Correlation]] data is senseless or not, we can use [[Linear Regression]] to check it out. 

## Using Seaborn Linear Regression
![[Pasted image 20220609160619.png]]

Here is the scatter plot for RAD index and TAX, read more in [[First Step of Data Exploration]]. We could see that their are outliers, data points that doesn't make any sense, to check the [[Linear Regression]] of this graph we could use [[Seaborn Module]] using `sns.lmplot(x= , y=, data= )`

```
import seaborn as sns

sns.lmplot(x='TAX', y='RAD', data=data)
plt.show()
```

![[Pasted image 20220609160144.png]]

We could see this show us a [[Positive Correlation]] but the scatter plot is messy making it invalid. After all, RAD is only an index. We could also refer to this as one of the examples of [[Correlations Problem on Linear Data|Anscombes quartet]] 