# Reference Type
In java, an example of this is a string, an array and an index. They are variables that are stored in the [[Heap]] which means when they are not used, they are treated as a garbage ready for collection.

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

obj1 === obj2 will output true, obj3 === obj1 will output false. WHY? Because it is not a [[Primitive Types]]. Reference type are things that the programmer creates. When we say obj2 = obj1, we are just referencing the [[Memory address]] to another object to get hold of that data. obj1 is not === to obj3 as they have different memory address or storage as said in [[Javascript Objects Equality]]
