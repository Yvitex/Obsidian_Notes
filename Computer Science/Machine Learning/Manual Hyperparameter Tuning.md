# Manual Hyperparameter Tuning
There are different types of [[Hyperparameter]] we could tweek in each model. And of course, we tune the [[Hyperparameter]] using the [[Validation Sets]]. 
In a [[Classification Machine Learning]] using [[Random Forest Classifier]], we could use these:

## Hyperparameters
[[Top Classification Model Hyperparameters]]

We could get more data by setting this code from the [[Machine Learning Algoritm|model]] object
```python
model.get_params()
```
![[Pasted image 20220802111233.png]]

To do this, after creating [[Three Sets in Code]], 

[[Fit the data to the model and make a prediction]] using the [[Validation Sets]]
```python
np.random.seed(42)
from sklearn.ensemble import RandomForestClassifier
model = RandomForestClassifier().fit(X_train, y_train)
y_valid_prediction = model.predict(X_valid)
```

[[(DM)Evaluation|evaluate]] the data, use a function for reusability
```python
def classif_anal(y_actual, y_preds):
    precision = precision_score(y_actual, y_preds)
    accuracy = accuracy_score(y_actual, y_preds)
    recall = recall_score(y_actual, y_preds)
    f1 = f1_score(y_actual, y_preds)
    
    info = {
        "Precision": round(precision, 2) * 100,
        "Accuracy": round(accuracy, 2) * 100,
        "Recall" : round(recall, 2) * 100,
        "f1": round(recall, 2) * 100,
    }
    
    for inform in info:
        print(f"{inform}: {info[inform]} %")
        
    return info
```

Use this function and compare the actual validation data to the prediction
```python
classif_anal(y_valid, y_valid_prediction)
```

![[Pasted image 20220802113557.png]]


Tweak the hyperparameters, experiment to make higher [[Accuracy]] than the baseline
```python
np.random.seed(42)
model = RandomForestClassifier(max_depth=9, n_estimators=40).fit(X_train, y_train)
y_prediction = model.predict(X_valid)
classif_anal(y_valid, y_prediction)
```

![[Pasted image 20220802114107.png]]

Use [[Random Seed]] to use the same order everutume you [[Fit the data to the model and make a prediction|fit()]]

We could also use for loop to aid the process.