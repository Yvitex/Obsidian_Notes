---
aliases: []
---
# Javascript Sort
This is a built in [[Sorting Algorithm]] in [[Javascript]]. There are many problems in using sort like it doesn't work with this:
```js
const array = [1, 51, 32, 72, 48, 2, 4]
console.log(array.sort())
```

![[Pasted image 20221006123340.png]]

See, this is not correct. It works well with string though, but with no special character like
```js
const array = ["apple", "moon", "banana"];
console.log(array.sort())
```

![[Pasted image 20221006123446.png]]

It doesn;t work well with spanish though like
```js
const array = ["único", "árbol", "cosas", "fútbol"];
console.log(array.sort())
```

![[Pasted image 20221006123840.png]]

This is because they are being converted into [[Unicode]] but only the first letter, if they are integer, they are being converted into string which is already a red flag. The example above composed of array with set of integers, 32 is less than 4 because:
```js
const check = "32".charCodeAt(0) < "4".charCodeAt(0);
```

![[Pasted image 20221006124433.png]]

There are several ways to fix this and they are all in the [documentaiton](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort). For example:
```js
const array = [1, 51, 32, 72, 48, 2, 4]
console.log(array.sort((a, b) => a - b))
```

Incase of string then:
```js
const array = ["único", "árbol", "cosas", "fútbol"];
console.log(array.sort((a, b) => a.localeCompare(b)))
```

![[Pasted image 20221006125930.png]]


# Metatags
###### Related: 
###### Tags: 
###### Source: 

---