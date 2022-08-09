# Plotting Feature Importance
After getting the coefficient values in a [[Logistic Regression]] model, or some other form of getting those [[Numpy Module|ndarrays]] of value, we need to transform it into a [[Dataframe (Pandas)|dataframe]], so save the values to a variable

```python
model = LogisticRegression(C=0.18420699693267145, solver="liblinear")
model.fit(X_train, y_train)

importance_feat = model.coef_
```

Transform it into a [[Python Dictionary]] using some mapping technique 
```python
importance_collection = dict(zip(df.columns, importance_feat.coef_[0]))
```

![[Pasted image 20220805101726.png]]

Store it to a dataframe
```python
feature_imp = pd.DataFrame(importance_collection.values(), index=importance_collection.keys())
```

Plot the data using a [[Bar Plot(Pd)]]
```python
feature_imp.plot.bar(legend=False)
```
![[Pasted image 20220805101940.png]]