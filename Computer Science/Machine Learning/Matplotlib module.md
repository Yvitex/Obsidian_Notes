# Matplotlib Module
To use this, we first need to import it

`import matplotlib.pyplot as plt`


## Making a linear plot
```
plt.plot(x, y)
plt.show()
```

## Making a scatter plot
```
plt.scatter(x, y)
plt.show()
```

## Labels
```
plt.ylabel()
plt.xlabel()
```

## 3d Space
```
fig = plt.figure(figsize=[20, 15])
ax = fig.add_subplot(projection="3d")
```

## Histogram with Pandas
```
plt.hist(pandas.series)
plt.show()
```

## Bar graph
```
plt.bar(row_list, height=height_list)
```

Related: [[Pandas]], [[Python Programming]]



