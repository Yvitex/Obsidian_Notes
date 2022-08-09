# 3 sets
We already knew about the [[Three Sets]] and the [[Splitting the Training and Testing Dataset]]. It is the same as in [[Deep Learning]]. We split this into 3 sets, in [[Kaggle]] competition, they provide the [[Test Sets]]  and [[Training Sets]] so we only need to worry about the [[Validation Sets]] and we could get it by spitting the [[Training Sets]] using the train_test_split method

```python
X = filename # contains all filepath of unstructued data
y = target # contains all the correct labels of each filename item
```

Split it
```python
from sklearn.model_selection import train_test_split

np.random.seed(42)
X_train, X_val, y_train, y_val = train_test_split(X, y, test_size=0.2)
```

If you have 10000 data sets, use only the 10% or 1000 or else, you will take ages. The best way is to create a slider method parameters, we could do this in [[Google Colab]] through `#param{}`

```python
NUM_INP = 1000 #param{type: "slider", min:1000, max:10222}

from sklearn.model_selection import train_test_split

np.random.seed(42)
X_train, X_val, y_train, y_val = train_test_split(X[:NUM_INP], y[:NUM_INP], test_size=0.2) # slice the sets
```



