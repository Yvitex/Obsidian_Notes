# Improving the Model
The first creation of the model is called [[Baseline Model]] and the first prediction of the [[Baseline Model]] is the baseline prediction. It will be the base of our  experiment in order to improve the [[Machine Learning Algoritm|model]] we have by tuning the [[Hyperparameter]]s . 

But before that, we might consider using other [[Machine Learning Algoritm|model]]s.

The workflow in doing this requires association with the [[Validation Sets]] meaning we must form [[Three Sets]] first. 

We could do this in 3 possible ways
- [[Manual Hyperparameter Tuning]]
- [[RandomSearchCV]]
- [[GridSearchCV]]


We could do this step by step $$Manual \rightarrow RandomSearch \rightarrow GridSearch$$
If you are using the [[Classification Report]] function manually created, use the return values to create a chart comparing the [[Machine Learning Algoritm|model]]s using [[Dataframe (Pandas)|dataframe]] and [[Bar Plot(Pd)]]

```python
data_merge = pd.DataFrame({"Manual": manual_data, "RandomSearchCV": rsc_data, "GridSearchCV": gsc_data, "Normal": normal_data})

plt.style.use("seaborn")
data_merge.plot.bar()
```

![[Pasted image 20220802163011.png]]