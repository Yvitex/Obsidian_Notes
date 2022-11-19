---
aliases: []
---
# Consensus Theorem
This simplify the boolean functions. 

$$AB + ĀC+BC = AB+ĀC$$


Solution:
First we use the [[OR gate]], we extract the A and its complement and multiply it to BC
$$AB + \bar AC + BC(A + \bar A)$$

BC multiply 1 is BC. Using the [[Distributive Law]], distribute BC to the A and the complement
$$AB + \bar AC + BCA + BC\bar A$$

Notice that we have similar variables to be extract using [[Distributive Law]]. Extract AB and Complement A and C
$$AB(1+C) + \bar AC(1 + B)$$

Using the [[Or Law]], we knew that 1 + Variable is equals to 1 and in [[And Law]], 1 and AB is equal to AB, therefore
$$AB + \bar AC$$


# Metatags
###### Related: [[Boolean Laws]]
###### Tags: 
###### Source: 

---