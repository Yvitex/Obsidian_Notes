---
aliases: [Pyramid of Doom, for await, Promise.all()]
---
# Promises
A [[Javascript]] concept that will let you execute a function after another, or do a promise that it will do something in the background. This is a good replacement for callback functions like this

```js
movePlayer(100, "left",  function(){
	movePlayer(20, "right",  function(){
		movePlayer(30, "left",  function(){
			movePlayer(100, "left",  function(){
			}
		}
	}
})
```

This is called the Pyramid of Doom. Calling callbacks one after another are unreadable and will just cause confusion, it is much more preferable to use Promises like this
```js
movePlayer(100, "left")
	.then(movePlayer(100, "left"))
	.then(movePlayer(100, "left"))
	.then(movePlayer(100, "left"))
```

This will execute the function asynchronously.
The basic object syntax of promises are
```js
const promise = new Promise((resolve, reject) => {
	if(true){
		resolve("Resolved")
	}
	else{
		reject("Rejected")
	}
})
```

Now, when we call this promise, we could use `then` to output a successful promise
```js
promise.then((data) => console.log(data))
```

This will output the thing that we put on resolve. We could return the value again and call it at the second `then` method
```js
promise
	.then((data) => data)
	.then((data2) => console.log(data2))
```

This will be the same output. So what if there is an error? We could call it with `catch` method
```js
promise
	.then((data) => data)
	.then((data2) => {
		throw Error;
		console.log(data2);
	})
	.catch(() => console.log("error"))
```

Catch will only catch an error that happens before it so it wont detect the error like this
```js
promise
	.then((data) => data)
	.catch(() => console.log("error"))
	.then((data2) => {
		throw Error;
		console.log(data2);
	})
```

If we have a catch block, then we must also have a `finally` block
```js
promise
	.then((data) => data)
	.then((data2) => {
		throw Error;
		console.log(data2);
	})
	.catch(() => console.log("error"))
	.finally(() => console.log("final end"))
```

Finally will execute with or without errors.

The basic function of Promises are used in [[API]]
```js
fetch("https://jsonplaceholder.typicode.com/comments")
	  .then(data => return data.json())
	  .then(dataJson => console.log(dataJson))
```

## Promise.all()
We could also execute multiple promise at once, suppose you want to execute this promises at the same time

```js
const promise = new Promise((resolve, reject) => {
	if (true) {
		resolve("Something");
	} else {
		reject("Rejected Ouch");
});

const promise2 = new Promise((resolve, reject) => {
	setTimeout(resolve, 300, "Hi");
});

const promise3 = new Promise((resolve, reject) => {
	setTimeout(resolve, 2000, "Hithen");
});

const promise4 = new Promise((resolve, reject) => {
	setTimeout(resolve, 3000, "Heathen");
});
```

We could call it by putting it inside an array and feed it inside the `Promise.all()`
```js
Promise.all([promise, promise2, promise3, promise4])
	.then(result => console.log(result))
```

What's special about this is that the promises above is already executed before we even write this method so the timeinterval is somehow useless unless you execute the codes at the same time, the promise will wait until all promises are done then print it out.

Two easiest way to simplify this is through `Promises.resolve()` and `Promises.reject()`
```js
const promise = Promise.resolve("Success")
promise.then((data) => console.log(data)) // output Success

const rejected = Promise.reject('failed')
rejected.catch(() => console.log("Oops"))
```

THis concept is heavily used to `fetch()` [[API]] request for multiple API calls where we wait until we get the data. 
```js
const request = [
	"https://jsonplaceholder.typicode.com/comments",
	"https://jsonplaceholder.typicode.com/posts",
	"https://jsonplaceholder.typicode.com/todos"
];
```

```js
Promise.all(request.map((data) => {
	return fetch(data).then((resp) => resp.json());
}))
	.then((data) => console.log(data));
```

## Promise.allSettled()

The main difference between this method and the `Promise.all()` is that Promise.all(), when it encounteres a rejected promise, it will not execute or continue. 
```js
const promise1 = new Promise((resolve, reject) => {
	setTimeout(resolve, 300, "Hi");
});

// Rejected promise
const promise2 = new Promise((resolve, reject) => {
	setTimeout(reject, 2000, "Hithen");
});

Promise.all([promise1, promise2])
	.then((data) => console.log(data)) // not execute
```

Instead, replace it with `allSettled`
```js
const promise1 = new Promise((resolve, reject) => {
	setTimeout(resolve, 300, "Hi");
});

const promise2 = new Promise((resolve, reject) => {
	setTimeout(reject, 2000, "Hithen");
});

Promise.allSettled([promise1, promise2])
	.then((data) => console.log(data)) // will output an array
```


## for await()
Alternatively we could use `for await`
```js
const getData = async function(){
	const arrayResp = await request.map((data) => fetch(data));
	for await(let response of arrayResp){
		const data = await response.json();
		console.log(data);
	}
}
```

# Metatags
###### Related: [[Javascript]]
###### Tags: 
###### Source: 

---