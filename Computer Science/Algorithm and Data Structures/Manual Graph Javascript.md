---
aliases: []
---
# Manual Graph Javascript
What we are trying to create are undirected, unweighted graph of this style
![[Pasted image 20221005110028.png]]

To do this create a simple constructor that will initialize the number of nodes and initialize an object storage.
```js
class Graph { 
  constructor() { 
    this.numberOfNodes = 0;
    this.adjacentList = {
    }; 
  } 
}
```

We are going to use storage because they are easier to handle and it have names. We will create a vertex then using this method where we will simply create a key in the adjacentList object that will contain an empty [[Array Data Structure]].
```js
addVertex(node){
	this.numberOfNodes++;
	this.adjacentList[node] = [];
}
```

We will then create the vertices that will connect this components, this will take 2 nodes to be connected
```js
addEdge(node1, node2){
	this.adjacentList[node1].push(node2);
	this.adjacentList[node2].push(node1);
}
```

That's all

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---