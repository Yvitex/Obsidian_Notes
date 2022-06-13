#  Seaborn's Multiple Graph
[[Seaborn Module]] has a lot to offer but running multiple graphs at once could take sometime depending on the machine with [[Pandas]] dataframe

## Scatter Plot
To do this, we simply use the function `sns.pairplot(dataframe)`

```
import seaborn as sns

sns.pairplot(data)
```

Data came from [[First Step of Data Exploration]] 

![[Pasted image 20220609164850.png]]

Here are all the scatter plots generated and we could not analyze each combinations.


## Linear Regression
We could create a simple multiple [[Linear Regression]] fast by using the same function, `sns.pairplot(data, kind='reg')` but using kind= reg.

```
import seaborn as sns

sns.pairplot(data, kind='reg')
```

![[Pasted image 20220609165055.png]]


Now we can crearly see the [[Correlation]]s of each combinations