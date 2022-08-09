---
aliases: [O(1)]
---
# O(1)
In [[Big O Asymptotic Analysis]] Means the operations are flat, no matter how big an array we are using, we are still doing one operation to a single input, for instance, the first value in an array.

![[Pasted image 20220730042047.png]]

What if we have this code that takes in the first 2 input in the array
```js
function takeTwo(array){
	console.log(array[0]);
	console.log(array[1]);
}
```

Each operation takes O(1) time
```js
function takeTwo(array){
	console.log(array[0]); //O(1)
	console.log(array[1]); //O(1)
}
```

Therefore there is O(2). But we round this off as constant time
```js
function takeTwo(array){
	console.log(array[0]); //O(1)
	console.log(array[1]); //O(1)
}

// O(2) is still O(1)
```

Simply O(1) is constant time.
