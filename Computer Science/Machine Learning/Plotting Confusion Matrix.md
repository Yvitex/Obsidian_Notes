# Plotting confusion Matrix
We could do this using the [[Seaborn Heatmap]], and we apply the value of the[[Confusion Matrix]] as an argument.
```python
from sklearn.metrics import confusion_matrix
conf_data  = confusion_matrix(y_test, y_preds)

import seaborn as sns

sns.heatmap(conf_data)
```

![[Pasted image 20220801121600.png]]


To make our lives easier and reusable, create a function with it
```python
def plot_conf_mat(conf_mat):
	sns.set(font_scale=1.5)
	sns.heatmap(conf_mat, annot=True)
	plt.xlabel("Actual Values")
	plt.ylabel("Predicted Values")

conf_mat_plot(conf_data)
```

![[Pasted image 20220801123857.png]]

