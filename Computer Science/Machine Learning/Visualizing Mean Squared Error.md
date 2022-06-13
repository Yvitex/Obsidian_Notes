# Visualization
Remember that a cost function depends on the parameter values or theta values and not the actual data itself. This will be the result of our visualization.  
  
The first thing we need to do is to create an initial theta values using linspace method just to create the surface of the graph![[Pasted image 20220605144744.png]]

This will create a one dimensional array which is not what we need, because we are plotting in a 3 dimensional graph, we need a 2 dimensional array to satisfy our plot. Therefore, we use a numpy, meshgrid method. Multiple parameter meshgrid returns a tuple of values that can be passed to multiple variables in sequence.

![[Pasted image 20220605144754.png]]

This will create a 2d array with symmetrical values.![[Pasted image 20220605144803.png]]

Will output (5, 5), which means 5 rows and 5 columns.![[Pasted image 20220605144812.png]]

Next is to create a placeholder for our cost function. Because it is a 2 dimensional placeholder that will contain the [[Mean Squared Error]] in the shape of (5, 5), we could do this by creating a 5 by 5 zeroes using [[Numpy Module|numpy zero method]].

![[Pasted image 20220605144820.png]]

np.zeros accepts a tuple with the length of rows and column.

Then we need to calculate the MSE of each combination of theta 0 and theta 1. We can do this by using a nested for loop and overriding our cost function containing zero with the resulting values
![[Pasted image 20220605144845.png]]

Now, create a 3d graph.
![[Pasted image 20220605144858.png]]

Note that gca method is already depricated. We use `.add_subplot()` instead. This will result into
![[Pasted image 20220605144911.png]]


Next is add the plot surface using .plot_surface(). This accepts theta 0, theta 1 and the means squared error. Remember that what we calculate in the cost function are the thetas and not x or y.

![[Pasted image 20220605144929.png]]

Now the plot will look like this

![[Pasted image 20220605144937.png]]

This happens because we only have 5 by 5 data. Increase the number of values into 200 by modifying nr_thetas and we will get

![[Pasted image 20220605144957.png]]

Now, to actually plot the gradient descent, we need to calculate the slope in each parameter. In order to do that, we need to get the partial derivative of the Mean Squared Error. If y hat is equivalent to the linear gradient formula, then the formula to be used is:
![[Pasted image 20220605145012.png]]

First formula is the partial derivative of mse with respect to theta 0  
Second formula is the partial derivative of mse with respect to theta 1  
  
Create a function that will calculate both of this values and return it as a numpy array. In the parameters, the third param will accept an array where var\[0] is theta 0 and var\[1] is theta 1

![[Pasted image 20220605145029.png]]


We could now let the machine learn through prediction supplyign it with a multiplier and an initial value

![[Pasted image 20220605145046.png]]

In here, the gradient function will accept the actual data x and y plus the initial guess as the thetas array.  
  
We could now print the resulting minimum theta0, theta1 and MSE of the minimum.

![[Pasted image 20220605145104.png]]

Now to plot this, we need to store the theta values and the MSE somewhere. Create a variable that will store the guesses and mse values in a form of an array. Make sure they have compatible shapes such as plot_vals mush be a 2d array with the shape of (1, 2) and mse_vals with shape of (1, 1) 2d array

![[Pasted image 20220605145118.png]]