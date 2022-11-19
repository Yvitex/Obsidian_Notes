---
aliases: []
---
# Recursion
It is a function that defines to itself. For instance, we create a functin and then we call that function inside of that function then it is a recursion. 
```js
function recurs(){
	recurs();
}
```

This are useful for traversing trees, where nodes contain children and children are parents that contain children. When we use the [[DOM]], we are using recursion. Using the command `ls -R`, when folders contain subfolders, then it will be shown as well. We use recursion heavily for repeated application. 

The problems in here is that it may cause a [[Call Stack|Stack Overflow]]. So how could we avoid this? 
In recursion their is a proper anatomy in construction:
- base case
- recursive case
- 2 return values

Base case is what will stop the recursion and wll return the value, recursive case will also contain a return value to bubble up the result from the base case. 

We can't do it like this:
```js
function recursion(){
	recursion();
}
```

We will create a base case where it will stop when 0 becomes greater than 3
```js
let counter = 0;
function recursion(){
	console.log(counter)
	if(counter > 3){
		return "done";
	}
	counter++; //increment
	recursion();
}
```

Unfortunately, when we call `recursion()`, it won't do anything, it won't return done because what we are basically doing is
```js
recursion(recursion(recursion(recursion(recursion()))))
```

When it finally hit return, tis will look like
```js
recursion(recursion(recursion(recursion("done")))
```

which doesn't work really. What we could do is to put another return key to the recursive call
```js
let counter = 0;
function recursion(){
	console.log(counter)
	if(counter > 3){
		return "done";
	}
	counter++; //increment
	return recursion();
}
```
![[Pasted image 20221005122648.png]]

Another problem when it comes to recursion is that it sometimes could lead of [[Exponential Time Complexity]] like when solving [[Fibonacci Recursion]] but there are ways to solve this like [[Memoization]] or [[Dynamic Programming]]. Some languages have also other ways of writing it so that it allows us to use recursion without increasing the [[Call Stack]]. 

The benefit of recursion is that it prevents code from repeating itself, and also make your code a lot cleaner and readable. The problem at this is as usual, the significant increase in the use of [[Call Stack]].

Anything that we could do on recursion we could do in iterative. 
Recursions are very useful when it comes to [[Tree Data Structure]] traversal. When doing this, always use recusion, there are also other problems that use recursion.
- Divide the problem into a number of subproblem that are smaller instancs of the same problem
- The instance of subproblem is identical in natyre
- Solution of subproblem could be combined to solve the main problem

Sounds like [[Divide and Conquer]] approach. These are also used in a number of [[Algorithm]]s such as:
- [[Merge Sort]]
- [[Quick Sort]]
- [[Searching Algorithm|Tree Traversal]]
- [[Searching Algorithm|Graph Traversal]]

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---