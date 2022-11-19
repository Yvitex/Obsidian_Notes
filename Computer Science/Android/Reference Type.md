---
aliases: [Pointer]
---
# Reference Type
In java, an example of this is a string, an array and an index. They are variables that are stored in the [[Memory Heap]] which means when they are not used, they are treated as a garbage ready for collection or [[Garbage Collection]]

![[Pasted image 20220617054451.png]]



The other way around to understand this is using an example with [[Javascript]] syntax
```js
console.log([] === [])
```

Will output false... and
```js
let obj1 = {
	value: 10
}

let obj2 = obj1

let obj3 = {
	value: 10
}
```

obj1 === obj2 will output true, obj3 === obj1 will output false. WHY? Because it is not a [[Primitive Types]]. Reference type are things that the programmer creates. When we say obj2 = obj1, we are just referencing the [[Memory address]] to another object to get hold of that data. obj1 is not === to obj3 as they have different memory address or storage as said in [[Reference Type]]

# Javascript Object
When is an object equivalent to another?
```js
let object1 = {name: "Miguel"};
let object2 = object1;

console.log(object1 === object2);
```

Will yields into `true` as they have the same [[Memory address]]. This is called a [[Reference Type]]
But, if we say that
```js
let object1 = {name: "Miguel"};
let object3 = {name: "Miguel"};

console.log(object1 === object3);
```

Will yield into `false`. Object3 have different [[Memory address]] than object1. Even if we have exactly the same key-value pairs, it will still not be the same as we are actually comparing [[Memory address]] and not the key-value pair itself. 