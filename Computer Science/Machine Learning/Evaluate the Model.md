---
aliases: [RocCurveDisplay()]
---
# Evaluation
We already knew this from [[(DM)Evaluation]]. We use a lot of metrics depending on the [[Machine Learning Algoritm|model]] we used

Fist create a [[ROC Curve]] plot the [[Plotting ROC Curve]]. There is a new way of plotting things using `RocCurveDisplay()`
![[Pasted image 20220804172008.png]]

## Params
- fpr : [[False positive]] rate
- tpr : [[True positive]] rate
- roc_auc : displays the [[Area Under Curve|roc_auc_score()]]
- estimator_name : accepts a string that will be displayed besides Auc score. 

Create then a [[Confusion Matrix]] and then [[Plotting Confusion Matrix]]
![[Pasted image 20220804172211.png]]

THis is important to know where the [[Machine Learning Algoritm|model]] is getting wrong often, in the [[False positive]] or the [[False negative]]?

Next is to create a [[Classification Report]]
![[Pasted image 20220805084630.png]]

As we already know, when [[False negative]] is 0, [[Recall]] would be 100, if [[False positive]] is 0, [[Precision]] would be 0. We could also refer to the [[Confusion Matrix]] we just created. 

Then create a graph represent the [[K-fold Precision Validation|cross_val_score()]] of [[Precision]], [[Accuracy]], [[Recall]] and [[F1 Score]]
![[Pasted image 20220805091553.png]]
![[Pasted image 20220805091602.png]]

![[Pasted image 20220805091612.png]]


