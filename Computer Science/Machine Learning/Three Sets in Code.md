# Three sets in code
We may want to use our [[Test Sets]] as a [[Validation Sets]] but to be more thourough, we could split it up to entirely 3 different sets. The [[Training Sets]], [[Validation Sets]] and [[Test Sets]]

Because we cannot use the usual [[Splitting the Training and Testing Dataset]] we must resort to manual [[Python Slicing]] and [[Shuffe Rows in Pandas|sample()]] methood that will randomize the [[Dataframe (Pandas)|dataframe]]

```python
dataframe_random = dataframe.sample(frac=1)
```

Split the data to [[(DM)Feature|feature]] and [[Target]]
```python
X = dataframe_random.drop("target", axis=1)
y = dataframe_random["target"]
```

Split the data to training, test and validation sets. Before that, create a number that will determine the amount of elements that will divide the sets
```python
training_amount = round(0.70 * len(X))
validation_amount = round(training_amount + 0.70 * len(X)) # we add training amount to start the slice from where the training amount have stopped
```

Split now
```python
X_train, y_train = X[:training_amount], y[:training_amount]
X_valid, y_valid = X[training_amount:validation_amount], y[training_amount: validation_amount]
X_test, y_test = X[validation_amount:], y[validation_amount:]

len(X_train), len(X_valid), len(X_test)
```

![[Pasted image 20220802112532.png]]


In the tuple we could see that X_train have the greatest number meaning our slicing works

