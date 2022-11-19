---
aliases: [Graph Traversal, Tree Traversal]
---
# Searching Algorithm
A kind of algorithm that checks and retrieve an existence of item inside a [[Data Structure]]. 

Here is some list of some kind of searching algorithm:
- [[Linear Search]]
- [[Binary Search]]
- [[Depth First Search]]
- [[Breadth First Search]]
- [[Dijkstra Algorithm]]
- [[Bellman Ford Algorithm]]

The last 2 [[Algorithm]]s are for [[Graph Data Structure]] and [[Tree Data Structure]], and not exactly for search but for traversing the nodes inside the trees. BEcause it is a traversal algorithm, then, it is obvious that the [[Big O Asymptotic Analysis|Time Complexity]] is always [[Linear  Time Complexity|O(n)]], we will use the 2 depending on the situation:

```
If you know a solution is not far from the root of the tree: BFS
If the tree is very deep and solutions are rare: BFS if time is your concern,DFS if space is your concern
If the tree is very wide: DFS
If solutions are frequent but located deep in the tree: DFS's main purpose
Determining whether a path exists between two nodes: DFS
Finding the shortest path: BFS
```

Somtimes, in an array, if they are already sorted, we could easily search an item using [[Divide and Conquer]] approach which is [[Logarithmic Time Complexity|O(log n)]]. 
For unsorted array, we might, possibly sort it first before searcging which could be [[Loglinear Time Complexity|O(n log(n))]] but most of the time, we'll just do a linear search which is [[Linear  Time Complexity|O(n)]].
If its a string, use [[Trie]].


# Metatags
###### Related: [[Algorithm]]
###### Tags: 
###### Source: 

---