---
aliases: [async, await]
---
# Async and Await
Is just another [[Promises]] in a different syntax, or syntactic sugar. Instead of writing the [[API]] calls like this
```js
fetch("https://jsonplaceholder.typicode.com/comments")
	  .then(data => return data.json())
	  .then(dataJson => console.log(dataJson));
```

We create an [[Async and Await|async]] method to make the function asynchronous or run in the background and inside it, we use [[Async and Await|await]] to do the processes synchronously

```js
async function requestData(){
	const data = await fetch("https://jsonplaceholder.typicode.com/comments");
	const extractJson = await data.json()
	await console.log(extractJson)
}

requestData()
```

It have longer syntax yet still it is readable. To create a catch, what we could do is simply encumber the processes in a Try and Catch Block
```js
async function requestData(){
	try{
		const data = await fetch("https://jsonplaceholder.typicode.com/comments");
		const extractJson = await data.json()
		await console.log(extractJson)
	}
	catch (err){
		console.log("ERR " + err)
	}
}

requestData()
```

To do this in multiple [[API]] calls like this
```js
const request = [
	"https://jsonplaceholder.typicode.com/comments",
	"https://jsonplaceholder.typicode.com/posts",
	"https://jsonplaceholder.typicode.com/todos"
];

Promise.all(request.map((data) => {
	return fetch(data).then((resp) => resp.json());
}))
	.then((data) => console.log(data));
```

We could apply an await in the Promise 
```js
const request = [
	"https://jsonplaceholder.typicode.com/comments",
	"https://jsonplaceholder.typicode.com/posts",
	"https://jsonplaceholder.typicode.com/todos"
];

async function multRequest(){
	const [comments, posts, todos] = await Promise.all(request.map((data) => 
									fetch(data).then(resp => resp.json())))
	console.log(comments);
	console.log(posts);
	console.log(todos);
}
```

With a catch block it look like this
```js
const request = [
	"https://jsonplaceholder.typicode.com/comments",
	"https://jsonplaceholder.typicode.com/posts",
	"https://jsonplaceholder.typicode.com/todos"
];

async function multRequest(){
	try{
		const [comments, posts, todos] = await Promise.all(request.map((data) => 
									fetch(data).then(resp => resp.json())))
		console.log(comments);
		console.log(posts);
		console.log(todos);
	}
	catch (err){
		console.log("ERR", err);
	}
}
```


# Metatags
###### Related: [[Promises]], [[Destructuring]]
###### Tags: 
###### Source: 

---