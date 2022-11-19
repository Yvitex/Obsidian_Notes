---
aliases: []
---
# Binary Search Tree
Is a common [[Data Structure]] that is specialized for searching data or numbers. 
![[Pasted image 20221003155625.png]]


Their are certain rules in building this type of [[Data Structure]], first of all, greater value goes always to the right, left is in a decreasing order. How we approach the searching mechanism is though that order, when an item we want to search is lesser value, then go to the left, if we want a greater value from the current node, go to the right. 

We could actually see this in action using this [website](https://visualgo.net/en/bst)

```ad-Notice
title: We only insert value in BST as a leaf
collapse: open
THere is no in between insertion in nodes

```

## Time Complexity
| Operation | Time Complexity                           |
| --------- | ----------------------------------------- |
| Lookup    | [[Logarithmic Time Complexity\|O(log n)]] |
| Insert    | [[Logarithmic Time Complexity\|O(log n)]] |
| Delete    | [[Logarithmic Time Complexity\|O(log n)]]|                                          |

For the best case, this is the time complexity, for the worst case, they are all [[Linear  Time Complexity|O(n)]]. Why? Because binary search tree could be unbalanced like this
![[Pasted image 20221003161349.png]]

We keep adding higher values that make it look like a [[Singly Linked List]]. In that case, the look up is automatically [[Linear  Time Complexity|O(n)]]. Like discussed before this is called <u>Unbalanced Binary Search Tree </u>and the previous is called <u>Balanced Binary Search tree</u> but there are also [[Algorithm]]s that could make or ensure a resulting Balanced Search Tree like [[AVL Tree]] or [[Red Black Tree]]

Why do we need to use it? How it is better than [[Array Data Structure]] or [[Hash Table]]?
It is better than array when it comes to lookup speed, insertion etc. While arrays are a [[Linear  Time Complexity|O(n)]], this are [[Logarithmic Time Complexity|O(log n)]] which is better. 
On the otherhand, while this data structure is slower than [[Hash Table]], it has an order, it preservers the relationship which is not applicable in [[Hash Table]]. We also have sorted data which is a plus. 

Now we could create our own [[Manual Binary Search Tree Javascript]]

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---