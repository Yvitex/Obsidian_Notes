# Spread Operator
Spread operator is the rest operator. (...)

```js
let num1 =  ['a', 'b', 'c'];
let num2= [1, 2, 3, ...num1];
```
output : \[1, 2, 3 ,  'a',  'b', 'c']

In a dictionary
```js
const fullName = {
	fName: "jhon",
	lName: "Licer"
}

const identification = {
	...fullname,
	id: 1, 
	contactNum: 123
}

```


This principle is heavily used in [[React]] to get again the previous values of a multiple variable state component. 
