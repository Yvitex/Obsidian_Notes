# Javascript Object
When is an object equivalent to another?
```js
let object1 = {name: "Miguel"};
let object2 = object1;

console.log(object1 === object2);
```

Will yields into `true` as they have the same [[Memory address]]. This is called a [[Pointer]]
But, if we say that
```js
let object1 = {name: "Miguel"};
let object3 = {name: "Miguel"};

console.log(object1 === object3);
```

Will yield into `false`. Object3 have different [[Memory address]] than object1. Even if we have exactly the same key-value pairs, it will still not be the same as we are actually comparing [[Memory address]] and not the key-value pair itself. 