# Async
Asynchronous programming simply means it runs on multi-thread, meaning the executions happen in parallel. Though there is an instance that this would also work in an [[Call Stack|single-threaded]] language like [[Javascript]] using the [[Javascript Run Time Environment]],
![[Pasted image 20220929121807.png]]

For instance, we could call setTimeout() to make some function 
```js
console.log("A");
setTimeout(() => {
	console.log("B")
}, 2000);
console.log("C");
```

This will execute in the following order, A, C then B. But if we set the time out value to 0,
```js
console.log("A");
setTimeout(() => {
	console.log("B")
}, 0);
console.log("C");
```

This will still execute in A, C B order. Why???
Each method will be done [[Synchronous programming|Synchronously]], each of them will go to the [[Call Stack]]

`A` will go to the call stack then deleted, after that, we have `B` on callstack. But because it uses setTimeout(), this method will be mounted to Web APIs and removed to call stack. C will then goes to the [[Call Stack]], executes then get deleted. Once the time runs out, for example, if we set it for 2000 milliseconds and it was finished, then it will go next to the callback queue and get the callback function inside of it, in our case an anonymous function which is `() => {console.log("B")}`. Event loop will then checks if there is something running on the [[Call Stack]] if none, this function will then goes to the [[Call Stack]] and excutes the function, it finds the console.log method and then call it to the call stack, execute then delete this method, then the anonymous function. 

Event loop is responsible for [[Javascript|Js event listener]].


This is complete opposite of [[Synchronous programming]]
