---
aliases: [Directed Graph, Undirected Graph, Unweighted Graph, Weighted Graph, Cyclic Graph, Acyclice Graph]
---
# Graph Data Structure
[[Tree Data Structure]] is a child of this data structure even  the linear ones like [[Singly Linked List]] or [[Doubly Linked List]]. This [[Data Structure]] are composed of nodes/vertices and edges which connects the nodes together. This is one of the most popular [[Data Structure]] in computer science and is used by many applications such as the social system of facebook, or google map to see the nearest possible route. 

## Types of Graph

There are many types of graph, too many in fact, but we could identity specific characteristic of a graph in few several ways:
- **Directed Graph**: sorta like twitter where one node points to other nde but that other node doesn't point to them, when you follow a person on twitter, they don't automatically follow you back. 
![[Pasted image 20221005034913.png]]

- **Undirected Graph**: like facebook where one nodes point to another and that other node points to them too. Having friends on facebook is a bidirectional system where if they friended you, you friended them
![[Pasted image 20221005035028.png]]

- **Unweighted Graph**: Normal graphs where we store information at the nodes
![[Pasted image 20221005035103.png]]

- **Weighted Graph**: We store information even at the edge. This are often used in efficient path finding or shortes path like google map
![[Pasted image 20221005035138.png]]

- **Cyclic Graph**: Are graphs that forms a circle or loop.![[Pasted image 20221005035350.png]]
- **Acyclic Graph**: Are graphs that doesn't form a circle
![[Pasted image 20221005035422.png]]

![[Pasted image 20221005035819.png]]

This graph is what we call DAGH or Directed Acyclic Graph which has direction, and acyclic used in [[BlockChain]] technology. 

## Approach in Constructing Graph

![[Pasted image 20221005042201.png]]

There are 3 ways on how we could approach building graphs:
- **Edge List**: Here we will create a 2 dimensional array, each array inside the array contains a node - node connection and it could only be a maxumum length of 2.  
```js
const edgeList = [[0, 2], [2, 3], [2, 1], [3, 1]]
```

So for the first array we have 0 and 2, this only means that 0 is conencted to 2 and 2 is connected to 0 cos it is undirected. We don't say \[1, 2] cos we already have \[2, 1] which is redundant to the edge list. 

- **Adjacent List**: Adjacent list is another 2d array that uses the indexes, honestly we could use nodes and objects in this case but we do that later. So if we are finding a connectior for node 0, the index 0 of that array will contain that connection. 
```js
const adjacentList = [[2], [2, 3], [0, 1, 3], [1, 2]];
```

- **Adjacent Matrix**: We will represent this using [[Binary]] combinations to represent the connected nodes
```js
const adjacentMatrix = [
	[0, 0, 1, 0],
	[0, 0, 1, 1],
	[1, 1, 0, 1],
	[0, 1, 1, 0]
]
```

Or as object such as
```js
const adjacentMatrix = {
	0: [0, 0, 1, 0],
	1: [0, 0, 1, 1],
	2: [1, 1, 0, 1],
	3: [0, 1, 1, 0]
}
```

Here is a good [website](https://visualgo.net/en/graphds) for graph visualization.
The main benefits of this [[Data Structure]] is that it is has relationship though the cons of using this is that  creating a graph that scales well will cost too much resournces and man power to be implemented. 
Now, here it is all you need to create your own [[Manual Graph Javascript]]

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---