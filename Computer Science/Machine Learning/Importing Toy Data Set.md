# Toy Data set
[[SciKitLearn]] have their Toy Data in their libraries and we just need to import it, Here is the [documentation](https://scikit-learn.org/stable/datasets/toy_dataset.html) that will tell you the list of modules we could use for example is the boston toy datasets.

```
from sklearn.dataset import load_boston

boston = load_boston()
boston_df = pd.DataFrame(boston["data"], columns=boston["feature_names"])
boston_df["target"] = boston["target"]
boston_df
```

![[Pasted image 20220731120221.png]]

