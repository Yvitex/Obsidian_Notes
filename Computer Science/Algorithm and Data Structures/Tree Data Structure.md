---
aliases: [Abstract Syntax Tree]
---
# Tree Data Structure
![[Pasted image 20221003060750.png]]

We already know what tree is and it has several parts:
- Root - 1 - origin
- Parent = \[1, 3] - node with children
- Child - \[2, 3, 4, 6, 7] - any node that came from a parent
- Leaf - \[2, 6, 7, 4] - outer most children
- Sibling - \[\[234], [6, 7]] - node that has a same parent

We use this data structure everywhere, for exampel in our [[DOM]] where HTML tag is the parent of the body and head, and they are sibling nodes. Drawing this, then we have the abstract syntax tree which is simply the conversion of a programming syntax to a tree diagram to make it understandable inside a computer
![[Pasted image 20221003061256.png]]


Commeting system is also a tree data structure where people could reply to another people and then reply to your message and so on. 

This is kinda like a [[Singly Linked List]]but instead of having multiple branches, linked list only runs at a linear line. One thing to keep in mind is that it is not like [[Doubly Linked List]], it cannot point to the parent, only to the child. 

Here are some list of tree data structure from [wikipedia](https://en.wikipedia.org/wiki/List_of_data_structures)
- [[Binary Tree]]
- [[Binary Heap]]
- [[Trie]]













# Metatags
###### Related: 
###### Tags: 
###### Source: 

---