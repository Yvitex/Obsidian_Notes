# Joblim Module
A recommended way of [[Save and Reload Training Model|model persistency]]. 


## Saving
```python
from joblib import dump, load

dump(model, filename="gsc_model_classifier.joblib")
```


## Loading
```python
model_imported = load(filename="gsc_model_classifier.joblib")
```