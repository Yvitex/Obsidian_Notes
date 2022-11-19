---
aliases: []
---
Is an iterative method to find the values of x, y, z in a [[System of Linear Equations]]. 
The very first thing that we need to do in this method is to arrange the equations in a diagonally dominant form  where the highest value in the first equation should have x as greatest, the second as y and the third as z. 
```
Raw Formulas
4x + 22y - 13z = -128
19x - 13y + 4z = 111
8x + 8y + 17z = 10

Diagonally Dominant
19x - 13y + 4z = 111 - highest in x
4x + 22y - 13z = -128 
8x + 8y + 17z = 10 - highest in z
```

Arrange it so that we could get the value of x
```
x = (111 + 13y - 4z)/ 19
y = (-128 - 4x + 13z) / 22
z = (10 - 8x - 8y) / 17
```

Starting from x, y, z value of 0 get the value of x y and z. For each iteration we will update the value of x y z with the previous resulting values














# Metatags
###### Related: 
###### Tags: 
###### Source: 

---