# Residuals
According to [[Residual Sum of Squares]] formula, individual data boils down to this formula $$residual = y - \hat{y}$$
Residual is the differece between actual data and the hypothesized data (predicted value). 
$\hat{y}$ could be anything, depending on our regression algorithm. In our case using [[Multivariable Regression]], $\hat{y}$ is equal to $$\hat{y} = \theta_0 + \theta_1RM + \theta_2NOX + \dots + \theta_nLSTAT$$
In our [[Bayesian Information Criterion]], we already removed, irrelevant [[Exploring the Data (Methodology)|feature]] therefore, we are left with this hypothetical regression. $$\hat{y} = \theta_0 + \theta_1RM + \theta_2NOX + \dots + \theta_{11}LSTAT$$
Remember that in a [[Linear Regression]] algorithm, $$\hat{y}= h_{\theta}(x)$$
```ad-note
This is a continuation from [[Bayesian Information Criterion]]

```

## Patterns
Once we calculated the residuals and plotted it in a scatter plot. We may see a pattern, if it has a pattern, then our model is bad. Here are some of the bad models with bad residuals. 

### Bad Patterns
![[Pasted image 20220623122554.png]]

![[Pasted image 20220623122607.png]]

![[Pasted image 20220623122616.png]]

![[Pasted image 20220623122647.png]]

![[Pasted image 20220623122658.png]]

![[Pasted image 20220623122708.png]]



### Good Patterns
![[Pasted image 20220623122758.png]]

![[Pasted image 20220623122806.png]]

```ad-Notice
collapse: open
Yes, a good residual pattern has no pattern. A normal pattern!

```

Click [this](https://www.youtube.com/watch?v=dQw4w9WgXcQ) to know more!!!

To create a plot for residual Patterm we first need to determine the plot for the Actual Data and Predicted values discussed in [[Plotting Linear Regression for Model with Training Dataset]]

