---
aliases: []
---
# Doubly Linked List

![[Pasted image 20220927061607.png]]

Unlike [[Singly Linked List]] which only have one pointers pointing to the next value, in [[Doubly Linked List]], we have 2 pointers, pointing to the next value and the previous value. This enables us to traverse the data backwards. THe merits to that is we could somehow reduce the [[Big O Asymptotic Analysis|time complexity]] of searching through it backwards and make it somehow O(n/2) though it will occupy more memory than [[Singly Linked List]]. 

| Operation | Time Complexity |
| --------- | --------------- |
| Prepend   |      [[Constant Time\|O(1)]]           |
| Append    |   [[Constant Time\|O(1)]]                |
| Lookup    |   [[Linear  Time Complexity\|O(n)]]              |
| Delete    |   [[Linear  Time Complexity\|O(n)]]              |
| Insert          |  [[Linear  Time Complexity\|O(n)]]               |

Still, lookup or search is technically [[Linear  Time Complexity|O(n)]].
We could crate our own [[Manual Javascript Doubly Linked List]]

# Metatags
###### Related: [[Singly Linked List]], [[Data Structure]], [[Reference Type]]
###### Tags: 
###### Source: 

---