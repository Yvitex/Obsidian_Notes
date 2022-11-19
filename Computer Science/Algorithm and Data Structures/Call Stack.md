---
aliases: [Stack Overflow, single-threaded]
---
# Call Stack
Is a [[Stacks|LIFO]] step by step excution of codes. Kinda like a [[Stacks]] for program execution. 

```js
console.log("A");
console.log("B");
```

Call stack will first excute the first console.log(), then delete it, it will then call the second console.log() then delete it.

For a more complex example. we have this code
```js
const plus = () => {
	const minus = () => {
		console.log("A")
	}
}
```

This will then call the plus function, call the minus function, then call the console.log(), after that, it will delete the console.log0, the minus function, then the plus function. Just imagine a pile of books in here, the last executed function will be the first one to delete. 

There is only one stack at [[Javascript]] so in that programming language, it is single-threaded, single-threaded simply means it has only one stack or it could only do one execution at a time. As the example above, we call the function one at a time in a chronological order, therefore this function is  [[Synchronous programming]]

## Stack Overflow
One concept might be familiar to you and it is called, Stack Overflow Error. This happens when you call functions infinitely until the call stack have not enough memory to hold the executions, we could recreate this using [[Recursion]]
```js
function call(){
	call(); // cause stack overflow
}
```

![[Pasted image 20220929114207.png]]



# Metatags
###### Related: [[Stacks]]
###### Tags: 
###### Source: 

---