---
aliases: [Closure]
---
# Memoization
Is a specific form of [[Dynamic Programming]]. We will store data to a [[CPU Cache|cache]], which in code could be a [[Hash Table]] so our retrieval is [[Constant Time|O(1)]]. 

How we could do this, for example is we have this function
```js
function add80(n){
	return 80 + n;
}
```

When we run it like this
```js
console.log(add80(5));
console.log(add80(5));
```

It will do the same thing over, but perhaps, it involves a very long calculation and it will took a long time for every call like
```js
function add80(n){
	console.log("20 min later...");
	return 80 + n;
}
// Output
// 20 min later... 85
// 20 min later... 85
```

It took us 40 min to complete the [[Runtime]]. What we could do is to create a [[CPU Cache|cache]]
```js
const cache = {};
function add80(n){
	console.log("20 min later...");
	return 80 + n;
}
```

We will check if the result exist inside the cache or not, if it is, return that value, if it is not, calculate a new one then put it inside the cache and return
```js
const cache = {};
function add80(n){
	if(n in cache){
		return cache[n];
	}
	else{
		console.log("20 min later...");
		cache[n] = 80 + n;
		return cache[n];
	}
}

// Ouput
// 20 min later... 85
// 85
```

So it took us only 20 min to do the operation, nice. But we don;t want to polute our global variable with our cahching mechanism. What to do is to yeah, put it inside the function
```js
function add80(n){
	const cache = {};
	if(n in cache){
		return cache[n];
	}
	else{
		console.log("20 min later...");
		cache[n] = 80 + n;
		return cache[n];
	}
}
// Ouput
// 20 min later... 85
// 20 min later... 85
```

But because we are reseting the cache for every function call, then it is useless. What to do is using the concept of Closures. We could do this by returning an anonymous function that contain the actual mechanism of the function. We also don't need the parameters to the outer function
```js
function add80(){
	const cache = {};
	return function(n){
		if(n in cache){
			return cache[n];
		}
		else{
			console.log("20 min later...");
			cache[n] = 80 + n;
			return cache[n];
		}
	}
}
```

Now, when we call the function like this
```js
const memoiz = add80()
```

Variable memoiz have the anonymous function as add80 returns it. We could do this
```js
const memoiz = add80()
console.log(memoiz(5))
console.log(memoiz(5))
```

![[Pasted image 20221012050819.png]]

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---