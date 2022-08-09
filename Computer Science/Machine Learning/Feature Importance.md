# Feature Importance
Different models have different ways to get the feature importance. We could simply search unto google how...
![[Pasted image 20220805100027.png]]

And according to the research, feature importance can be extracted from [[Logistic Regression]] using the [[Coefficient]] variable

```python
model = LogisticRegression(C=0.18420699693267145, solver="liblinear")
model.fit(X_train, y_train)

model.coef_
```

![[Pasted image 20220805100608.png]]

Then we could move on on [[Plotting Feature Importance]] like this
![[Pasted image 20220805101950.png]]


We could that sex have high effect on the target data. if we  [[Comparing Data|crosstab()]] it
![[Pasted image 20220805102113.png]]

We could see that if the sex is female, their is a 72 out of 96 chance or 75% chance that she have a heart disease, therefore it have a [[Negative Correlation]] that if the sex label is lower, then the higher chance that she have a heart disease as confirmed by our [[Correlation Matrix]] in the [[Comparing Features]] section. What baseically true is that the data shows that sex have an effect of how the machine will predict the result. 

Cholesteror on the other hand seems to have no effect on the prediction therefore meaning we need to have more data for it, or investiaget it. If there is a greater feature importance as shown in the coefficient values, then we might improve it more.

![[Pasted image 20220804113114.png]]

