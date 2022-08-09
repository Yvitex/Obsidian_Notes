---
aliases: [roc_auc_score()]
---
# Area Under Curve
![[Pasted image 20220801103645.png]]

Area under the curve is literraly the area under the [[ROC Curve]]. [[SciKitLearn]] already provide us with a method to do this
```python
from sklearn.metrics import roc_auc_score
roc_auc_score(y_test, y_preds[:, 1])
```

This will accept 2 parameters, the actual value and the positive column of the predicted value or [[Y Hat]]
![[Pasted image 20220801104535.png]]

This is the case under [[Binary Classification]]
