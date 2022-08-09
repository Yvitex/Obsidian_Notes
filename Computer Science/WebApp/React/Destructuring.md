# Destructuring
Is a way to assign a value to a variable from a complex [[Data Structure]].
There are 2 types of destructuring and they are

## Array destructuring
We can assign variables from an array like this
```js
const [first, second, third, ...rest] = [1, 2, 3, 4, 5]; 
```

In this case, first = 1, second = 2, third = 3, rest = \[4, 5]. It depends on the position of the values in the arrays.

## Object destructuring
Is a way to destructure the values enclosed inside a curly braces
```js
const typesOfMatter= {
	solid: "Have a definite shape and volume",
	liquid: "The shape depends on its container",
	gas: "Have no definite shape",
	cola: "Sexy, curvy body" 
}

const {solid, liquid, gas, cola} = typesOfMatter;
```

The value will depend on the keyword used so the variables must be the same exact spelling used for the keys. We could also change the name for each variable such as

```js
const {solid : metal, liquid : water, gas : fart, cola : umaru} = typesOfMatter;
```

Or we have layers of object inside an object such as
```js
const layersOfTrash = {
	astolfo : {
		Umaru : {
			Jotaro : "Is not Trash"
		}
	}
}
```

Then we could do this
```js
const {astolfo : {Umaru : {Jotaro}}} = layersOfTrash;
```

Combining this 2 types, for an instance that you have an object with an array inside such as
```js
const layered = {
	list : [1, 2, 3 ];
}
```

We could extract this by:
```js
const {list: [first]} = layered;
```

Then first is equals to 1. 



![[clipart407079.png]]
