---
aliases: []
---
# Binary Search
So, we have this [[Array Data Structure]]
![[Pasted image 20221010115841.png]]

What do you think is a more efficient way to search through it that using a [[Linear Search]]? We use a [[Divide and Conquer]] approach, we first get the value of the center, then decide from where we want to go and divide it again into half. 

Consider this new set of new numbers
![[Pasted image 20221010122136.png]]

Perhaps we want to search for 34, we first get the center which is 9. Because 9 is less than 34, we go to the right and divide it once again into half, this case, we get 34 and 34 matches the value that we want. Here we only do 2 iterations. In actuality, we are doing this in [[Binary Search Tree]] mode. ![[Pasted image 20221010122513.png]]
At this rate, we have a [[Big O Asymptotic Analysis|Time Complexity]] of [[Logarithmic Time Complexity|O(log n)]]. The problem here is that we need to first sort the data









# Metatags
###### Related: [[Binary Search Tree]], [[Sorting Algorithm]], [[Searching Algorithm]]
###### Tags: 
###### Source: 

---