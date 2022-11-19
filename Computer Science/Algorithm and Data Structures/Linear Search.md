---
aliases: []
---
# Linear Search
A type of [[Searching Algorithm]] usually used in an [[Array Data Structure]]. Best case it could have a [[Big O Asymptotic Analysis|Time Complexity]] of [[Constant Time|O(1)]] but the worst case could be [[Linear  Time Complexity|O(n)]]. 

![[Pasted image 20221010115841.png]]

We will scan each item of the array until we found the item we are looking for. [[Javascript]] have some owned implementation of [[Searching Algorithm]] such as
```js
let arr = [1, 2, 3];
// 1.
arr.indexOf(2);

// 2.
arr.findIndex(function(res){
	return res === 2;
}); 

// 3.
arr.find(function(res){
	return res === 2;
}); 

// 4.
arr.includes(2);
```

The more efficient way to search in an [[Array Data Structure]] is by what we call a [[Binary Search]] 


# Metatags
###### Related: 
###### Tags: 
###### Source: 

---