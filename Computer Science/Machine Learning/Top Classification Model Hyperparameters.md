## Top Classification Model Hyperparameters 
- max_depth - integer
- max_features - could be auto
- min_samples_leaf 
- min_samples_split - probably 1 - 10, coulf be a float but see this info from [stack overflow](https://stackoverflow.com/questions/67532613/how-to-define-min-sample-split-and-min-sample-leaf-in-decision-tree-regresso#:~:text=So%20values%20should%20go%20between,0.01%2C%200.1%2C%201). Basically it must not be more than the row size
- n_estimators -integer


We use this via trial and error. Here are more information in the [documentation](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html) of [[SciKitLearn]]

