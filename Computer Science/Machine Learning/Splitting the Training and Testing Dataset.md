# Splitting the training and testing dataset
What's going here is that we are separating the training and testing data and shuffling them accordingly. It is important to shuffle the data into randomness to erase the clear pattern where the [[Exploring the Data (Methodology)|data point]] is allocated


## Code
We can simply do this by using [[SKLearn Module]]'s `train_test_split()` function
We first need to import this module from sklearn's `model_selection`

```
from sklearn.model_selection import train_test_split
```

Then we separate the [[Exploring the Data (Methodology)|target]] column and the other features. `.drop()` method will remove the row or column in the [[Pandas|dataframe]]. 

```
from sklearn.model_selection import train_test_split

price = data["PRICE"]
features = data.drop('PRICE', axis=1)

```

Now is the time to split  the data out. `train_test_split()` method returns a tuple with 4 elements. We need to declare 4 variables to catch it. This accepts some parameters, first is the features, next is the target, then the test_size that will indicate the ratio of the number of test variable over total length of features, and random state that is entirely optional.

```
from sklearn.model_selection import train_test_split

price = data["PRICE"]
features = data.drop('PRICE', axis=1)

X_train, X_test, y_train, y_test = train_test_split(features, price, test_size=0.2, random_state = 10)
```

In our case, we have an 80/20 ratio, 80 for training data and 20 for test data as we specified on`test_size=0.2`  

```
print(len(X_train)/len(features))
```

will print: 0.7984189723320159

```
print(len(X_test)/len(features))
```

will print: 0.2015810276679842

this justify the 80:20 ratio. 


Now, we can [[Calculate Linear Regression using Training Dataset]]
