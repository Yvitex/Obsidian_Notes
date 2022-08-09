---
aliases: [Data preparation]
---
# Data Preparation
Is the most first part of the [[Scikitlearn Workflow]] and even the [[Machine Learning Frameworks]]

There are 3 things that we need to do in this section:
1. [[Imputation or Deletion]] as they don't provide value
2. [[Convert classification string values into Numerical Data]] like [[Float Dollar String to Integer]]
3. Split the data into 2 separate variable into [[(DM)Feature|feature]] and label or [[Target]]

$$Clean Data \rightarrow Transform Data \rightarrow Reduct Data$$

First is [[Import Data from CSV to Dataframe]] using [[Numpy Module]]
```python
import pandas as pd

heart_dis = pd.read_csv("heart-disease.csv")
heart_dis
```

![[Pasted image 20220729173200.png]]

If there is not missing values or there is no string to be converted into integers, proceed into
Choosing your [[Target]], the rest would be the feature. We need to use the [[Delete Columns|drop()]] to separate this into 2 separate variable
```python
X = heart_dis.drop("target", axis=1)
X.head()
```

![[Pasted image 20220729173821.png]]

The target column disappear from our [[Dataframe (Pandas)|dataframe]]
```python
y = heart_dis["target"]
y.head()
```
![[Pasted image 20220729173857.png]]

Y already contain it.
[[Splitting the Training and Testing Dataset]] is already given in this case where we could use [[SciKitLearn]]'s built in function. Remember the [[Three Sets]], in a simpel data like this, we  can use 2

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
```

Checking the X_train variable
```python
X_train.head()
```
![[Pasted image 20220729173717.png]]

We could see that it is in random order so that the machine would not notice the data pattern and cause an [[Overfitting]]. Or i don't know.

If we look at the shape of each of the variables
```python
X_train.shape, X_test.shape, y_train.shape, y_test.shape
```
![[Pasted image 20220729174151.png]]

The original lenfth of the which is 303 when we do `len(X)` , data frame is reduced because we set the test size by 20% meaning the [[Training Sets]] will have 80% as opposed to [[Test Sets]] with 20%

