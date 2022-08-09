---
aliases: [O(n^2)]
---
# O(n^2)
This is a time complexity often relates to nested loops. 
```js
let arrays = [1, 2, 3, 4, 5]

function(arrays) {
	for (let i = 0; i < arrays.length; i++){
	  for (let j = 0; j < arrays.length; j++){
	    if(arrays[i] == arrays[j]){
	      continue;
	    }
	    console.log(`Pairs: ${arrays[i]} ${arrays[j]}`)
	  }
	}
}
```

We go through the same input twice, nested with each other. This will be represented as O(n * n) or O(n^2)

 ![[Pasted image 20220731045449.png]]


As we could see on the diagram, If we have 2 elements, the operation would be 4 and if there is 3, then it will rise in square and would be 9 total operations. 