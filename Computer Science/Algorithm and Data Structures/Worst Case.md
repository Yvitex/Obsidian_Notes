# Worst Case
Is one of the  [[Big O Reading Rules]] where we assume the worst case scenario

```js
let array = ["a", "b", "nemo", "c", "d", "e", "f", "g", "h", "i"]

function matcher(array){
	for(let i = 0; i < array.length; i++){
		if(array[i] == "nemo"){
			console.log("Found Nemo")
		}
	}
}

matcher(array)
```

In this case,w e are running the function in O(n) specifically O(10), we could make it more efficient by cutting the loop as soon as it found nemo
```js
let array = ["a", "b", "nemo", "c", "d", "e", "f", "g", "h", "i"]

function matcher(array){
	for(let i = 0; i < array.length; i++){
		if(array[i] == "nemo"){
			console.log("Found Nemo");
			break;
		}
	}
}

matcher(array)
```

But Big O doesn't care. Instead of Big O(3), it is still Big O(10)

