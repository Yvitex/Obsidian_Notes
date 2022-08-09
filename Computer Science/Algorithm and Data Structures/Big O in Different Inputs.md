# Different Inputs
```js
function compressBoxed(boxes1, boxes2){

boxes1.forEach(function(boxes){
	console.log(boxes)
})

boxes2.forEach(function(boxes){
	console.log(boxes)
})
}
```

For this [[Big O Reading Rules]], because we have different input array looping through and we don;t know the specific number on each one of them, we represent it through a variable but instead of saying [[Linear  Time Complexity|O(n)]], we say that it is O(a + b) because we have 2 different inputs. 

```js
function(arrays, array2) {
	for (let i = 0; i < arrays.length; i++){
	  for (let j = 0; j < arrays2.length; j++){
	    if(arrays[i] == arrays[j]){
	      continue;
	    }
	    console.log(`Pairs: ${arrays[i]} ${arrays[j]}`)
	  }
	}
}
```

Instead of [[Quadratic Time|O(n^2)]], this would be O(a * b)

