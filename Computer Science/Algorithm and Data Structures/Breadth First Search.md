---
aliases: []
---
# Breadth First Search
In this kind of traversal, we are first starts in the root node, proceed from left to right nodes
![[Pasted image 20221011100414.png]]

The root node is 9, we proceed to traverse to the children starting from left, to right. The sequence is as follows \[9, 6, 12, 1, 4, 34, 45]

![[Pasted image 20221011100528.png]]

This consumes a lot of memory because we need to track down each nodes. 
All traversals in [[Tree Data Structure]] and [[Graph Data Structure]] are [[Linear  Time Complexity|O(n)]] when it comes to speed, but the key takeaway of this [[Searching Algorithm]] is that this is good to find the shortest part in the tree and graph, it could be fast if we knew that the node we are looking for is somewhere near the top or root. The problem on the other hand is that it requires a lot of memory. 

In code, it would look like this inside a [[Manual Binary Search Tree Javascript]].
```js
// Create another method for BFS
bfs(){
	
}
```

Create 3 variables, the first will store the root, the second is the final result, the third is the [[Queue]]
using [[Array Data Structure]]. We will push the root to the [[Queue]] first
```js
bfs(){
	let temp = this.root;
    const final = [];
    const queue = [];

	queue.push(temp);
}
```

Now, while there is something in the queue, then we will overwrite the temp with this, if the value of the temp have a left and right pointer, we will input that children to the queue which increase our memory. Push the temp.value tot he final array

```js
bfs(){
	let temp = this.root;
    const final = [];
    const queue = [];

	queue.push(temp);
    while(queue.length > 0){
      temp = queue.shift();
      final.push(temp.value);
      if(temp.left){
        queue.push(temp.left);
      }
      if(temp.right){
        queue.push(temp.right);
      }
    }

  return final;
}
```

Return the final array. With [[Binary Search Tree]] like this
```js
//     9
//  4     20
//1  6  15  170
```

We have an output that is: \[9, 4, 20, 1, 6, 15, 170]

There is also a [[Graph Data Structure]] version of this, we could use this [site](https://visualgo.net/en/dfsbfs) to visualize what is happening
![[Pasted image 20221011163347.png]]

When we select 0 as the source of our algorithm, what we will first search is its nearby node which is 1, then 2 then 3. Then it will check other nodes the same way after. Like we said before, this is good in finding the shortest path avaiable between nodes.



# Metatags
###### Related: 
###### Tags: 
###### Source: 

---