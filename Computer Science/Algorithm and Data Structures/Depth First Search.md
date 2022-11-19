---
aliases: []
---
# Depth First Search
![[Pasted image 20221011101116.png]]

This is a kind of [[Tree Data Structure]] and [[Graph Data Structure]] traversal that starts from the root, goest to the left to the deepest left node, come back to the parent node with unexplored children then go to the deepest part of that unexplored children.

So in here, we start at root node 9, goes to 6, then 1. We go back to 6 then expre the children which is 4, we go back to the root node after this and expre the rest. The sequence is \[9, 6, 1, 4, 12, 34, 45]. In fact, this arrangement or orders of element in the array is only a type of how we could return the traversed tree. We have 3 types:
Consider this [[Binary Search Tree]]
```js
//     9
//  4     20
//1  6  15  170
```
- Inordered: we return the items in the array from left, then parent, then right from bottom level to the root so \[1, 4, 6, 9, 15, 20, 170]
- Preorder: we return it as an array from root, going to the left and deeper, jumpt to the next branch \[9, 4, 1, 6, 20, 15, 170]
- Postorder: we return the array where children come first before the parent, \[1, 6, 4, 15, 170, 20, 9]

The purpose of preorder and post order is their use for recreating a tree with the same values. 

See this sequence
![[Pasted image 20221011101620.png]]

The [[Big O Asymptotic Analysis|Time Complexity]] of this is [[Linear  Time Complexity|O(n)]], what makes this unque is the fact that this could be so slow when searching for a node that is near the root, probably because it will deep dive to a branch first before going to another. The benefit is that this requires less memory than [[Breadth First Search]]. 

This is how we will imprement DFS with code:

## In Order

We will utilize the power of [[Recursion]]. Create a function that will call this [[Searching Algorithm]] inside the [[Binary Search Tree]]. Return a function that will call the real [[Recursion]]
```js
dfsInOrder(){
	return this.depthInOrder(this.root, []);
}
```

Create this recursive function, go to the deepest left child if there is. After we done that, we will push this value of the node to the array we set in the argument. Then go to the right child of the node.
```js
depthInOrder(node, data){
if(node.left){
	this.depthInOrder(node.left, data);
}
data.push(node.value);
if(node.right){
	this.depthInOrder(node.right, data);
}
	return data;
}
```

For this [[Binary Search Tree]], we have
```js
//     9
//  4     20
//1  6  15  170

// The output is : [1, 4, 6, 9, 15, 20, 170]
```

## Pre Order

This is the same as above, create a function.
```js
dfsInOrder(){
	return this.depthInOrder(this.root, []);
}
```

Next, just copy the function in the in order and replace the name. The only change the position of where we will push node, in this case, we will push the node before we do a recursive call.
```js
depthPreOrder(node, data){
	data.push(node.value);
	if(node.left){
	  this.depthPreOrder(node.left, data);
	}
	if(node.right){
	  this.depthPreOrder(node.right, data);
	}
	return data;
}
```

```js
//     9
//  4     20
//1  6  15  170

// The output is : [9, 4, 1, 6, 20, 15, 170]
```

## Post Order

Do the same as before, but now, we will push the node after we traverse in the left and right child
```js
dfsPostOrder(){
	return this.depthPostOrder(this.root, []);
}

depthPostOrder(node, data){
	if(node.left){
	  this.depthPostOrder(node.left, data);
	}
	if(node.right){
	  this.depthPostOrder(node.right, data);
	}
	data.push(node.value);
	return data;
}
```

```js
//     9
//  4     20
//1  6  15  170

// The output is : [1, 6, 4, 15, 170, 20, 9]
```

How exactly does this work?? [[Call Stack]]. Each function is being stacked and executed in [[Stacks|LIFO]] principle, where it will go traverse the item first before executing the push method to the array. In this case, if we have so many levels or the height of our tree is very long, then we are using a lot of our memory. The [[Space Complexity]] is equivalent to O(height of the tree). 

There is also a [[Graph Data Structure]] version of this, we could use this [site](https://visualgo.net/en/dfsbfs) to visualize what is happening
![[Pasted image 20221011163846.png]]

In dfs, we go as deep as we can in one branch of the [[Graph Data Structure]] before going to another. This won;t find the shortest path but it will tell us if the path exist or not, this is good to use in maze problems. 

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---