# Evaluation
"What define sucess for us?" To work with [[Machine Learning]], we need to understand that it is an experiment, meaning there might be unlimited ways we could do this so we need to set a parameter on when we will stop. For example, if our [[Machine Learning Algoritm|models]] have 90% accuracym then we don't need to go further.

Here are all of the [metrics](https://scikit-learn.org/stable/modules/model_evaluation.html) available at [[SciKitLearn]]

For example, if we wanna build a machine that will detect when the heart disease, then we must set the accuracy to 99% because it is an important task,

But how do we measure an accuracy in [[Machine Learning]]? We use different kinds of metric to do this.

| Classification                        | Regression                      | Recommendation |
| ------------------------------------- | ------------------------------- | -------------- |
| [[Classification Report]]             | [[Mean Absolute Error]]         | Precision At K |
| [[K-fold Precision Validation]]       | [[Mean Squared Error]]          |                |
| [[Area Under Curve]] or [[ROC Curve]] | Root Mean Squared Error         |                |
| [[Confusion Matrix ]]                 | [[K-fold Precision Validation]] |                |
|                                       |      [[R_Squared]]                             |                |


The most Basic evaluation method you might encounter while working with [[SciKitLearn]] is the [[Score Accuracy Measure]]
