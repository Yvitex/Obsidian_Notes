# Mean Squared Error
  
## Formula is:
![[Pasted image 20220605144306.png]]

Where x is an array of values. Y_hat is equivalent of saying `regr.predict(x)`, where regr is an object of `LinearRegression()` from sklearn module.

![[Pasted image 20220605144319.png]]

## Converting the MSE formula into code
![[Pasted image 20220605144356.png]]

![[Pasted image 20220605144402.png]]

At which we summed the values inside the sqaure before multiplying it to the 1/n. Other way of calculating the same function in one line of code is just by simply using a method from sklearn. 

![[Pasted image 20220605144415.png]]

![[Pasted image 20220605144420.png]]

This method will output the same values as our function. In addition, we could also shortcut calculating our y_hat by simply saying

![[Pasted image 20220605144444.png]]

Next is [[Visualizing Mean Squared Error]]
