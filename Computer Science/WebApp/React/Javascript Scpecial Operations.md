---
aliases: [map, filter, reduce, find, findIndex]
---

# JS Function

## Map Function
Used in an array to change their values or something
```js
var numbers = [3, 56, 2, 48, 5];

const newNumbers = numbers.map(function(number){
	return number * 2;
})
```

Output: (5) [6, 112, 4, 96, 10]

It also have an index parameter
```js
var numbers = [3, 56, 2, 48, 5];

const newNumbers = numbers.map(function(number, index){
	return number * 2;
})

```


## Filter
As the name suggest, it filters the array. So when what when our condition is true, the element is returned to the variable
```js
var numbers = [3, 56, 2, 48, 5];

let newNumber = numbers.filter(function(params){
return params < 10;
})

console.log(newNumber)
```

Output: (3) [3, 2, 5]

It could also read index per iteration
```js
var numbers = [3, 56, 2, 48, 5];

let newNumber = numbers.filter(function(params, index){
return index != 1;
})

console.log(newNumber)
```

## Reduce
This needs 2 parameter, the current number and the accumulator, thisi only a for loop that will combine something, either by subtraction or addition even multiplication. 
```js
var numbers = [3, 56, 2, 48, 5];

let newNumber = numbers.reduce(function(accumulator, currentNumber){
return accumulator += currentNumber
})

console.log(newNumber)
```

## Find
Will find an element in an array that will satisfy the condition. This will only get the first element that will satisfy the condition
```js
var numbers = [3, 56, 2, 48, 5];

let newNumber = numbers.find(function(params){
	return params < 10;
})

console.log(newNumber)
```

Output: 3

## FindIndex
Similar to find, but index
```js
var numbers = [3, 56, 2, 48, 5];

let newNumber = numbers.findIndex(function (params) {
return params < 10;
});

console.log(newNumber);
```