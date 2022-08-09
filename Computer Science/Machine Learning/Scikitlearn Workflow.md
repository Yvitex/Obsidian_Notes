# Scikit Learn Workflow
![[Pasted image 20220729124650.png]]

- [[Get the Data Ready]]
- [[Pick a Model]]
- [[Fit the data to the model and make a prediction]]
- [[(DM)Evaluation]]
- [[Improve through Experimentation]]
- [[Save and Reload Training Model]]
- [[Merge All Steps]]


## Get the Data
We do this using [[Pandas]] [[Dataframe (Pandas)|dataframe]]
```python
import numpy as np
import pandas as pd

data = pd.read_csv("file.csv")
data.head()
```

![[Pasted image 20220729162153.png]]

## Pick Model
Using [[SciKitLearn]] module.  Import it and instatiate to anew object
```python
from sklearn.ensemble import RandomForestClassifier

clf = RandomforestClassifier()
```

## Fit data to the Model
Before we do that,  we need to determine what are the [[Exploring the Data (Methodology)|feature]], and what is the target. Split them into 2 dataset using the [[Delete Columns|drop()]] method
```python
X = data.drop("target", axis=1)
y = data["target"]
```

we need to create a separate set called [[Three Sets]], the training, the test and the validation sets
```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)
```

Then we could  fit the X_train and y_train together
```python
clf.fit(X_train, y_train)
```

We could use the X_test to output the [[Prediction]]
```python
y_preds = clf.predict(X_test)
```

![[Pasted image 20220729162221.png]]

## Evaluation
We have 3 ways to do this, first is the [[Fit the data to the model and make a prediction|score()]] method
```python
clf.score(X_test, y_test)
```
![[Pasted image 20220729162638.png]]

Means we have 82% accuracy
Other ways are using the [[Confusion Matrix]], [[Classification Report]], and accuracy score, Here we are testing between y_test and predicted y or y_preds
```python
from sklearn.metrics import classification_report, confusion_matrix, accuracy_score

classification_report(y_test, y_preds)
confusion_matrix(y_test, y_preds)
accuracy_score(y_test, y_preds)
```

## Improve Model
we could adjust the [[Hyperparameter]] using a loop for testing
```python
np.random.seed(42) # Removing this will change the result everytime you run

for i in range(10, 100, 10):
	print(f"Tring to model with {i} estimators...")
	clf = RandomForestClassifier(n_estimator=i).fit(X_train, y_train)
	print(f"Model accuracy on test set: {clf.score(X_test, y_test) * 100:.2f}%")
```

:.2f is a [[Classic Python Shortcut]] for round(x,  2)
![[Pasted image 20220729164232.png]]

## Save the Model
We use picke in this kind of situation. dump() to save and load() to load
```python
import pickle
pickle.dump(clf, open("something.pkl", "wb"))
```

To load
```python
load_model = pickle.load(open("something.pkl", "rb"))
```


