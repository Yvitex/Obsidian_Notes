# PLotting ROC Curve
we use the [[Matplotlib module]] in this case, the quick  [[Creating Data and Plot|plt.plot()]] method. To make our lives easier, we may create a function to create a modular and reusbale code

```python
from matplotlib.pyplot as plt

def roc_plot(fpr, tpr):
	plt.plot(fpr, tpr, color="orange", label="ROC")
	plt.plot([0, 1], color="blue", linestyle="--", label="guessing")
	plt.xlabel("False Positive Rate (fpr)")
	plt.ylabel("True Positive Rate (tpr)")
	plt.legend()
```

Now execute the code
```python
roc_plot(fpr, tpr)
```

![[Pasted image 20220801103247.png]]


Analyzing this graph, we could say that the [[Machine Learning Algoritm|model]] we have done good as it is above the guessing line. Under the guessing line indicate that there is an error.

