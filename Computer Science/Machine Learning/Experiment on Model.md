# Experiment
This is where all [[Tuning a Model]], [[Improve through Experimentation]] takes place.

To achieve this in [[Manual Hyperparameter Tuning]], we could create a loop and compare the resulting values to one another, we save it into an array  for later use

This website has some good guides regarding what [[Hyperparameter]] to tweak [press here](https://machinelearningmastery.com/hyperparameters-for-classification-machine-learning-algorithms/#:~:text=Logistic%20regression%20does%20not%20really,with%20different%20solvers%20(solver).&text=Regularization%20(penalty)%20can%20sometimes%20be%20helpful.&text=Note%3A%20not%20all%20solvers%20support%20all%20regularization%20terms.)

```python
train_score = []
test_score = []

neighbors = range(1, 21)

knn = KNeighborsClassifier()

for i in neighbors:
    knn.set_params(n_neighbors=i)
    
    knn.fit(X_train, y_train)
    
    train_score.append(knn.score(X_train, y_train))
    test_score.append(knn.score(X_test, y_test))
```

Then we plot it using [[Creating Data and Plot|plt.plot()]]
```python
plt.plot(neighbors, train_score, label="Train Score")
plt.plot(neighbors, test_score, label="Test Score")
plt.title("Test and Train Score Comparison in KNeighborClassifier", fontdict={"fontsize":15})
plt.xlabel("N_neighbors")
plt.ylabel("Score Value")
plt.legend()

print(f"Maximum Value it could have is {max(test_score) * 100:.2f}%")
```

![[Pasted image 20220804132131.png]]


After this, we could try some [[GridSearchCV]]
![[Pasted image 20220804162736.png]]

![[Pasted image 20220804162748.png]]

These are some tips regarding [what parameters to change](https://machinelearningmastery.com/hyperparameters-for-classification-machine-learning-algorithms/#:~:text=Logistic%20regression%20does%20not%20really,with%20different%20solvers%20(solver).&text=Regularization%20(penalty)%20can%20sometimes%20be%20helpful.&text=Note%3A%20not%20all%20solvers%20support%20all%20regularization%20terms.)
Here are some that is used in this case

```python
log_reg_grid = {
    "C": np.logspace(-4, 4, 50),
    "solver": ["liblinear", "sag"],
}


rand_for_grid = {
    "n_estimators": np.arange(1, 1000, 50),
    "max_depth": [None, 3, 5, 10],
    "min_samples_split": np.arange(2, 20, 2),
    "min_samples_leaf": np.arange(1, 20, 2)
}
```

Then try a [[GridSearchCV]]
![[Pasted image 20220804164617.png]]

