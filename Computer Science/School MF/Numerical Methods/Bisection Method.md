---
aliases: []
---
# Bisection Method
Is one of the famous [[Bracketing Method]] technique. And because it is some kind of a bracketing method, we will guess 2 initial values first that probably, have the roots, and the symptoms of having the roots is when there is a sign change.

First step is to choose 2 values that when substituted, will have different signs
![[Pasted image 20220922153042.png]]

This will be our left and right bracket. We will then get the midpoint of these 2 values.
![[Pasted image 20220922153129.png]]

Substitute the equation using the midpoint.
Now, if the resulting y value is negative, we choose the different portion that is positive then vice versa. 
![[Pasted image 20220922153313.png]]

This will be our new bracket.
So for example we have this equation:
$$f(x) = e^{-x} - x = 0$$
Choose 2 initial values that when substituted, will have different signs. We will chose 0 and 1.

| i   | xl  | xr  | f(xl) | f(xr)  | xm   | f(xm) |
| --- | --- | --- | ----- | ------ | ---- | ----- |
| 0   | 0   | 1   | 1     | -0.632 | 0.5  | 0.107 |

We could see that there is a sign change in our first iteration, we get the midpoint which is 0.5 and because the resulting equation is 0.107 we choose the side that is negative and that side is 1. Our left bracket then will be 0.5 and the right as 1, we will get the midpoint once again and repeat the process until satisfied

| i   | xl  | xr  | f(xl) | f(xr)  | xm   | f(xm) |
| --- | --- | --- | ----- | ------ | ---- | ----- |
| 0   | 0   | 1   | 1     | -0.632 | 0.5  | 0.107 |
| 1   | 0.5 | 1   | 0.107 | -0.632 | 0.75 | -0.287|

These will go into a loop.


# Metatags
###### Related: [[Bracketing Method]]
###### Tags: 
###### Source: 

---