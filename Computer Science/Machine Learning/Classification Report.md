---
aliases: [classification_report()]
---
# Classification Report
Shows the accuracy, recall and precision. In [[SciKitLearn]], we have a way to create this using the `classification_report()` method
```python
from sklearn.metrics import classification_report

print(classification_report(y_train, y_preds))
```

![[Pasted image 20220801131400.png]]

[[Precision]]
[[Recall]]
[[F1 Score]]
Support - the amount of frequency or accurence of 0 and 1 in the actual data.
[[Accuracy]]
[[Macro AVG]]
[[Weighted AVG]]

This method is very useful when trying to measure the [[Accuracy]] of imbalanced data, it will show the bias in data. 

Precision, recall, f1 score and accuracy could also be used in different way using direct function
```python
from sklearn.metrics import recall_score, accuracy_score, f1_score, precision_score
```

We could use this to create our own function
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


## Params
- Actual y value
- [[Y Hat]]

