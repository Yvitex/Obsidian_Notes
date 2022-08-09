# JS Performance Operator
```js
let array = new Array(1000).fill("nemo")

function matcher(array){
	for(let i = 0; i < array.length; i++){
		if(array[i] == "nemo"){
			console.log("Found Nemo")
		}
	}
}

matcher(array)
```

The [[Runtime]] of this wil be slow because we are finding a value from a series of 1000 values. We could measure the time using performance operator

```js
let array = new Array(1000).fill("nemo")

function matcher(array){
	let count0 = performance.now() 
	for(let i = 0; i < array.length; i++){
		if(array[i] == "nemo"){
			console.log("Found Nemo")
		}
	}
	let count1 = performance.now() 
	console.log("Performance: " + (count1 - count0) + " milliseconds")
}

matcher(array)
```

![[Pasted image 20220730035122.png]]

If we add more arrays up to 100000
![[Pasted image 20220730035211.png]]

It took us 14 seconds to do it. 
This is a very inaccurate way to measure the performance of a certain function or [[Algorithm]], But in our case, the [[Big O Asymptotic Analysis]] we are using is just [[Linear  Time Complexity]]

