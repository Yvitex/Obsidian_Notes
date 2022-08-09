# Baseline Model
Is a model we first created.
Perform [[Splitting the Training and Testing Dataset]]. We could create a dictionary of [[Machine Learning Algoritm|model]] and then loop through that dictionary via function in order to automatically fit and score data and compare which one is the best model we could use.

```python
X = heart_dis.drop("target", axis=1)
y = heart_dis["target"]

np.random.seed(42)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

models = {
    "LogisticRegression": LogisticRegression(),
    "KNeighborsClassifier": KNeighborsClassifier(),
    "RandomForestClassifier": RandomForestClassifier()
}

def fit_and_score(model, X_train, X_test, y_train, y_test):
    """
    This thing will fit and score the data to our model dictionary
    """
    
    # Random Seed 42
    np.random.seed(42)
    # Score Container
    model_score = {}
    
    # Loop through the array
    for model_name, model in model.items():
        model.fit(X_train, y_train)
        # Model Score
        model_score[model_name] = model.score(X_test, y_test)
        
    return model_score
```
![[Pasted image 20220804124002.png]]

According to the resulting data, [[Logistic Regression]] might be the best regression to the job. [[Regression Machine Learning]]

Plot this using a [[Matplotlib Bar Graph]]
![[Pasted image 20220804124227.png]]



