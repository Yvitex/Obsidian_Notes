# Pickle Module
Use to serialzie a python object or for [[Save and Reload Training Model|model persistency]]

## Writing Binary
```python
import pickle

pickle.dump(model, open("filename.pkl", "wb")) # means write binary
```


## Loading Binary
```python
model = pickle.load(open("filename.pkl", "rb"))
```

