---
aliases: []
---
# Garbage Collection
Works around [[Reference Type]] variables. When we delete a variable that is used to reference a value to another variable like this:
```js
const a = {value: 10};
const b = a;
delete a;
console.log(b);
```

b will still output {value: 10} but not because we create a new value for it before deleting a. We do this because the [[Memory address]] that stores the object value is not garbage collected as it knows that it is still being used somewhere by another variable. But once we assign a new value to that object: 
```js
const a = {value: 10};
const b = a;
delete a;
b = "{value: 10} is now deleted"
console.log(b);
```

b is now equal to a string as the object value is unused and deleted from the memory or [[Memory Heap]]


# Metatags
###### Related: [[Memory address]], [[Reference Type]], [[Singly Linked List]], [[Memory Heap]], [[Random Access Memory|ram]]
###### Tags: 
###### Source: 

---