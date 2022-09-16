# Visualizing Correlations
Here we use the [[Seaborn Module]] and [[Matplotlib module]] to create a heatmap of some sort that will tell us how strong the correlation is depending on its color.

First. Import the modules
```
import seaborn as sns
import matplotlib.pyplot as plt
```

Now create a heat map by using this seaborn method sns.[[Seaborn Heatmap|heatmap()]], this will accept the correlation datframe from [[Pandas]]

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.heatmap(data.corr())
plt.show()
```

Output: ![[Pasted image 20220606164728.png]]
We can largen it using the matplotlib methods,
`yticks()` `xticks()` `figure(figsize=[w, h])`

```
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=[13, 10])
sns.heatmap(data.corr())
plt.yticks(size=14)
plt.xticks(size=14)
plt.show()
```

![[Pasted image 20220606164933.png]]

The color is terrible, we can change this using `cmap=` in heatmap

```
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=[13, 10])
sns.heatmap(data.corr(), cmap="coolwarm")
plt.yticks(size=14)
plt.xticks(size=14)
plt.show()
```

![[Pasted image 20220606165108.png]]

Now, the color is more terrible than before. We can apply a [[Masking a DataFrame in Half|mask]] as one of the named parameters using `mask=` 
```
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=[13, 10])
sns.heatmap(data.corr(), cmap="coolwarm", mask=mask)
plt.yticks(size=14)
plt.xticks(size=14)
plt.show()
```


![[Pasted image 20220606165226.png]]


We can also set the text values of the correlation and resize it using `annot=` and `annot_kwr={}`

```
import seaborn as sns
import matplotlib.pyplot as plt

plt.figure(figsize=[13, 10])
sns.heatmap(data.corr(), cmap="coolwarm", mask=mask, annot=True, annot_kwr("size: 14"))
plt.yticks(size=14)
plt.xticks(size=14)
plt.show()
```

![[Pasted image 20220606165357.png]]


## Conclusion
![[Pasted image 20220605153907.png]]

- TAX and INDUS have high correlation, taxes are higher to places with lots of business
- TAX and RAD have a very high correlation, but this is a false alarm information because RAD unit is an index, it is discrete rather than continuous
- Another example of discrete values is at CHAS, it is only a [[Binary]] data with 2 possible values
- If we analyze our price which is our target, the lowest correlation we have is CHAS, but because it is a discrete value, we neglect it. The next lowest is the DIS, it is close to [[No Correlation|0]], furthermore,
- DIS and INDUS have a negative correlation. When distance from employment center increase from the houses, the businesses decrease which makes sense as usually, area with high business activities are also accompanied with high number of employment centers. The higher the distance from the employment center, the lower the industry the area is


## With these conclusion, we have a problem to solve
- Does including both DIS and INDUS makes the data better or worse? If it does not add any explanatory values, then it is better to be excluded.
- 