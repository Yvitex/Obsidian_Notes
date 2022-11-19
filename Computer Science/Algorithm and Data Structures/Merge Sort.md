---
aliases: []
---
# Merge Sort
A very efficient [[Sorting Algorithm]] better than [[Quadratic Time]]. It has the [[Big O Asymptotic Analysis|Time Complexity]] of [[Loglinear Time Complexity|O(n log n)]]

```ad-Attention
title: T'is what they call good algorithm
collapse: open
Use this [[Sorting Algorithm]] if you don't care about [[Space Complexity]]. 

```


![[Pasted image 20221007142727.png]]

How this works, we will divide a list of numbers into half. 
![[Pasted image 20221007142803.png]]

We will divide it firther into half![[Pasted image 20221007142824.png]]
We will divide this again until it became an individual piece
![[Pasted image 20221007142859.png]]

Now we will comapre the first two items and switch them as necessary
![[Pasted image 20221007142934.png]]

Next is the second pair and so on. ![[Pasted image 20221007143007.png]]

Now we will compare the first 2 groups per individual index. 
![[Pasted image 20221007143047.png]]

Do the same to the second group![[Pasted image 20221007143109.png]]

We will combine this then with their individual indexes
![[Pasted image 20221007143141.png]]

See, looks like a [[Tree Data Structure]]
Here we will utilize the concept of [[Recursion]]. The code to do this is:

First create a base case, the base case will execute when the array is individualized. 
```js
function mergeSort(array){
	if(array.length == 1){
		return array;
	}
}
```

Split the array in half
```js
function mergeSort(array){
	if(array.length == 1){
		return array;
	}
	const half = Math.floor(array.length); use Floor so there is no decimal
	let left = array.slice(0, half); // slice array from 0 to half
	let right = array.slice(half); // slice array from half to end
}
```

Create another function where we will transfer these left and right array, this function is responsible for merging them
```js
function mergeSort(array){
	if(array.length == 1){
		return array;
	}
	const half = Math.floor(array.length); use Floor so there is no decimal
	let left = array.slice(0, half); // slice array from 0 to half
	let right = array.slice(half); // slice array from half to end

	return merge()
}
```

We'll do a recursive approach that will individualize the original array, and we will use this to transfer to the merge function
```js
function mergeSort(array){
	if(array.length == 1){
		return array;
	}
	const half = Math.floor(array.length); use Floor so there is no decimal
	let left = array.slice(0, half); // slice array from 0 to half
	let right = array.slice(half); // slice array from half to end

	return merge(mergeSort(left), mergeSort(right));
}
```

Create that function, create 2 variables that will track the index of left and right. Al;so create a storage array
```js
function merge(left, right){
	let array = [];
	let leftIndex = 0;
	let rightIndex = 0;
}
```

Create a while loop that will merge these arrays, this loop will not stop until you finished scanning all indexes in the left and right array
```js
function merge(left, right){
	let array = [];
	let leftIndex = 0;
	let rightIndex = 0;
	while(leftIndex < left.length && rightIndex < right.length){
	
	}
}
```

Inside here, we will create a comparison that if either of the 2 is less than the other, it is the first one to be pushed in the new array
```js
function merge(left, right){
	let array = [];
	let leftIndex = 0;
	let rightIndex = 0;
	while(leftIndex < left.length && rightIndex < right.length){
		if(left[leftIndex] < right[rightIndex]){
			array.push(left[leftIndex]);
		}
		else{
			array.push(right[righIndex]);
		}
	}
	const storage = left.slice(leftIndex), right.slice(rightIndex);
	return array.concat(storage); // will merge the rest to the pushed array;
}
```

Now, we will return the merged values from the new array. As we could see, in merge sort, the time compelxity both worst and best case is [[Loglinear Time Complexity|O(n log(n))]] but the [[Space Complexity]] is [[Linear  Time Complexity|O(n)]] and that is the downside of this [[Algorithm]]. 

# Metatags
###### Related: 
###### Tags: 
###### Source: 

---