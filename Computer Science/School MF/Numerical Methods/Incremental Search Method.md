---
aliases: []
---
# Incremental Search Method
We need 3 things in this equation. First is the initial guess $x_0$. For each iterations, we will increase the value of x with a fixed step $\vartriangle x$  

So for example, we have this formula:
$$x^2 - x - 1 = 0$$

Out initial guess is $x_0 = 1.5$
And out delta x is $\vartriangle x = 0.005$

We will substitute the equation with out initial guess
| x_0   | f(x)      |
| ----- | --------- |
| 1.5   | -0.25     |
| 1.505 | -0.239975 |
| 1.510 | -0.2299   |
| ...   | ...       |
| 1.615 | -0.006775 |
| 1.620 | 0.044     |

Notice that the sign changes between 1.615 and 1.620. We will reduce the delta x value by half and then start the process once again until we get the closest number to 0. 

# Metatags
###### Related: [[Finding the Roots of Non Linear Equation]], [[Bracketing Method]]
###### Tags: 
###### Source: 

---