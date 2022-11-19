---
aliases: []
---
# Binary Heap
Is a common [[Tree Data Structure]] from the class [[Memory Heap]]
```ad-Attention
title: Binary Heap is Not Memory Heap
collapse: open
This is just a coincidence so they are never related

```

The main difference between this data structure and [[Binary Search Tree]] is their arrangement. While we could insert numbers in [[Binary Search Tree]], in binary heap, we could insert anything even strings and they are ordered based on priority. 

Orders are in either Max Heap or Min Heap![[Pasted image 20221004161110.png]]

Max heap when the root is the highest value, and descends each level below. Min heap is the inverse where the lowest value is the root and ascend each level below. 

| Operation | Time complexity                           |
| --------- | ----------------------------------------- |
| Lookup    | [[Linear  Time Complexity\|O(n)]]         |
| Insert    | [[Logarithmic Time Complexity\|O(log n)]] |
| Delete    | [[Logarithmic Time Complexity\|O(log n)]] |


We could see that the loopup is quite slow compared to [[Binary Search Tree]], it is because in this [[Data Structure]], there is no such thing as arrangement, so we need to traverse each node to find what we want. 

The edge of binary heap is when we do comparative operations such as getting all values above 33, then we could grab faster than [[Binary Search Tree]].

The rest of the operations are [[Logarithmic Time Complexity]] but here is the twist, In a max heap, when we are tying to insert values that is so low, we are actually have the time complexity of [[Constant Time|O(1)]]. 
![[Pasted image 20221004161812.png]]

We simply need to put it as a leaf. But worst case is when we are tying to insert a value that is higher than the root, in this case we have a [[Logarithmic Time Complexity]] in our hand. We will first insert the new node as a leaf, but then compare it with the parent and if it is greater than value than the parent, it will bubbles up. 

What is the benefit os using binary Heap? Usually, we would only use this if we are only interested of using the minimum (in case of Min Heap) or maximum value (in case of Max Heap). They are also used in constructing [[Priority Queues]]. Unlike [[Binary Search Tree]], they could never go unblanced because there is no order for nodes and we always input data from left to right, though some data may need to bubble up. This saves memory better than BST. It is also have faster inserts which could be [[Constant Time|O(1)]] or [[Logarithmic Time Complexity|O(log n)]].  

Here is the visualization for [binary heap](https://visualgo.net/en/heap?slide=1)

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---