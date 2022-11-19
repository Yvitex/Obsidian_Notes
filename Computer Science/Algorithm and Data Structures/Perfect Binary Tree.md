---
aliases: []
---
# Perfect Binary Tree
This is totally different from [[Full Binary Tree]], This is a type of binary tree that each parent could only have 2 childs, nothing more and nothing less. 

![[Pasted image 20221003145700.png]]

There are 2 interesting things about binary trees:
- Each level double the previous level. So when the root is 1, the next layer would have 2 node, the next layer would have 4 or simply, (2 ^ layer) when root is layer number 0. 
- The number of nodes in a layer is the sum of all previous nodes plus 1 or $$\sum{nodes + 1}$$ which is why the second layer is precisely all the previous nodes plus 1 (3 + 1)

What this simply implies is that the nodes doubles every layer. 
We could calculate the total number of nodes by just knowing the number of layers with this formula $$Nodes = 2^{height} - 1$$ Height is the number of levels, so if there are 3 levels (0, 1, 2 layer) then there are 7 nodes in total. 

What makes this [[Data Structure]] so good is the fact that it is optimized more than what an [[Array Data Structure]] could hope for. Rather than iterating on all items in that [[Data Structure]], we only iterate over the levels, so if there are 7 nodes, we find an item only with 3 steps, and we already know that on each layer, we are doubling what we already have so we could actually find an item in 15 nodes with only 4 steps, this is very efficient when it comes to [[Big O Asymptotic Analysis|time complexity]].

These are their operations, and we could see that they are very efficient
| Operation | Time Complexity                           |
| --------- | ----------------------------------------- |
| Lookup    | [[Logarithmic Time Complexity\|O(log n)]] |
| Insert    | [[Logarithmic Time Complexity\|O(log n)]] |
| Delete    | [[Logarithmic Time Complexity\|O(log n)]]|                                          |

log(n) basically equates to the height or the number of step rather than the number of items which make it very efficient. 


# Metatags
###### Related: [[Binary]]
###### Tags: 
###### Source: 

---