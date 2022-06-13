# Seaborn Module
A very good plot module that is based on [[Matplotlib module]]

## Set-up
```
import seaborn as sns
```

## Creating a Histogram with PDF
```
sns.histplot(panda.series, bins=50, kde=True, color="red")
plt.show()
```
[[Probability Density Function|PDF]] means probability density function

## Scatter Plot
```
sns.jointplot(x=x_dataseries, y=y_dataseries, s=300, height=10)
```

## Linear Regression
```
sns.lmplot(x=x_dataseries ,y=y_dataseries, data=data_frame)
```




