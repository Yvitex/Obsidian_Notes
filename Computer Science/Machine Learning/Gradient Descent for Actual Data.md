# The Real Cost Function  Residual Sum of Squares  vs [[Descriptive Statistics using Python|Mean]] Squared Error

![[Pasted image 20220605142449.png]]
[[Residual Sum of Squares|RSS]] is a fine function for calculating the minimum cost of a function but the number may grow too large, and sometimes, might cause an overflow error. To counter this, we add some elements to our function, and that is by multiplying the equation with 1/n, where n is the number of data points. The equation looks like this  
  
![[Pasted image 20220605142454.png]]

This is called MSE or [[Mean Squared Error]]. As the name suggest, we calculate the [[Descriptive Statistics using Python|mean]] of the points by dividing the whole equation by the total number of data points.

Next step is to perform a [[Linear Regression]]