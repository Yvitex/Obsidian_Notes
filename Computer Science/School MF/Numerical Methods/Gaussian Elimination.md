---
aliases: [Row Reduction]
---
# Gaussian Elimination
Is an [[Algorithm]] for solving [[System of Linear Equations]] made by Carl Friedrich Gauss. This involves converting [[Augmented Matrix]] to [[Row Echelon]] form and then back substituting them in order to get the vlaue of the variables. 

We convert [[Augmented Matrix]] to [[Row Echelon]] using Elementary Row Opertions which are:
- Swap - swap the current rows with the chosen row
![[Pasted image 20221013150646.png]]
- Scale - divide the current row
![[Pasted image 20221013150544.png]]
- Pivot - use the scale of another row and add it to the current
![[Pasted image 20221013150625.png]]

Those are the basic operations.

Example:
```
2x + 12y + 17z = -32
-3x - 7y - 8z = 6
x + 4y + 6z = -7
```

Convert this into augmented matrix:
![[Pasted image 20221013145859.png]]


Now, to transform the [[Augmented Matrix]] to [[Row Echelon]], the first row must have the header of 1. Because we already have a header 1 in the third row like in the above image, just swap it.
$$R_1 \leftrightarrow R_3$$

![[Pasted image 20221013150823.png]]

The second row must have a first value of 0, a header of 1. What we could do is to use the pivot operation using the first row. Multiply it by 3 and add the result to the second row. 
$$3R_1 + R_2 \rightarrow R_2$$
![[Pasted image 20221013151112.png]]

The result would be
![[Pasted image 20221013151842.png]]

We do the same for row 3, we use the first row, multiply it by -2, then add it to the row 3
$$R_3 - 2R_1 \rightarrow  R_3$$
![[Pasted image 20221013152239.png]]

Result would be
![[Pasted image 20221013152258.png]]

Now, because we need 1 as the header for the second row, we use the scale operation, in which we will divide the row by 5. 
$$1/5R_2 \rightarrow  R_2$$
![[Pasted image 20221013152422.png]]

The result would be
![[Pasted image 20221013152521.png]]

Now we use the second row in order to make the third have a second column 0. 
$$R_3 - 4R_2 \rightarrow R_3$$
![[Pasted image 20221013152727.png]]

![[Pasted image 20221013152749.png]]

Now, we will scale it so that the header is 1.
$$-1/3R_3 \rightarrow R_3$$
![[Pasted image 20221013152849.png]]

Now, we are going to back substitute it. Convert it into linear equation with variable x , y, z:
```
x + 4y + 6z = -7
y + 2z = -3
z = 2
```

We already knew that z is 2, so we could subtitute it to the second linear equation, 2 x 2 = 4
```js
x + 4y + 6z = -7
y + 4 = -3 -> y = -3 -4 -> y = -7
z = 2
```

We knew that y = -7, substitute it to the first equation
```js
x + 4(-7) + 6(2) = -7 -> x - 28 + 12 = -7 -> x = 28 -7 - 12 -> x = 9 
y = -7
z = 2
```

So the value of our variables are
```
x = 9 
y = -7
z = 2
```

Check it with the original equations
```
2(9) + 12(-7) + 17(2) = -32
-3(9) - 7y(-7)- 8(2) = 6
9 + 4(-7) + 6(2) = -7
```


# Metatags
###### Related: 
###### Tags: 
###### Source: 

---