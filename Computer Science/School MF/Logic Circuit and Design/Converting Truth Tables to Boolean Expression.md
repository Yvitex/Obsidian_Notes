---
aliases: [Product of Sum, Sum of Product]
---
# Converting Truth Tables to Boolean Expression

There are 2 ways to do this and they are Product of Sum and Sum of Product

## Sum of Product

![[Pasted image 20220927120739.png]]

We do this by converting each bits to an expression where y will result into 1. The forst binary is 010 and this is equivalent to not(a) . b . not(c). If bit is false, we will convert it into not() so it is A!BC! the same goes for 111. We will multiply each bits and add them later therefore Sum of product

## Product of Sum

![[Pasted image 20220927121006.png]]

We do the inverse. We will get the values that produce false or 0. So in our first binary, we have 011, if the [[Bit]] is 1, then it is a not(1) ro produce 0 output with [[OR gate]] so it is A + B! + C!, the same goes for the second argument. We will then multiply this additional later on hence product of sum.












# Metatags
###### Related: 
###### Tags: 
###### Source: 

---



