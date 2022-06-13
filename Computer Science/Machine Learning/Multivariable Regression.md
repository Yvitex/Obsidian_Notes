# What is Multivariable Regression?
In our past [[Linear Regression]] model, we use a simple model to calculate the hypothetical line of data. The formula for that is $$\hat{y} = \theta_0 + \theta_1x$$
- where $\hat{y} = h_\theta x$
- $\theta_0$ is the intercept
- $\theta_1$ is the slope
- $x$ is the descriptive variable or independent variable

In multivariable regression, we consider multiple $\theta_1x$ values.
## Formula
$$\hat{y} = \theta_0 + \theta_1x_1 + \theta_2x_2 + \dots + \theta_nx_n$$
Accordinly, x is our [[Exploring the Data (Methodology)|features]] or independent variable so we could say $$\hat{y} = \theta_0 + \theta_1RM + \theta_2NOX + \dots + \theta_nLSTAT$$
Based on the data of example data sheet [[First Step of Data Exploration|Boston Houses]]

Now, to calculate this, we first need to [[Splitting the Training and Testing Dataset]]

