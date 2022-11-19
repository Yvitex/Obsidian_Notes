---
aliases: []
---
# Manual Stack Javascript
We could do this in 2 ways, using [[Singly Linked List]] or with [[Array Data Structure]]:

## Linked List

We could start by tracking the top and bottom nodes of the linked list. The top part will be the last input, and the part that will be removed because it is easier to track than the bottom.
```js
class Stack {
  constructor() {
    this.top = null;
    this.bottom = null;
    this.length = 0;
  }
}
```

We have 3 main method and they are, push, pop, peek. We go first with peek. This is simply outputing the last value which is the top
```js
peek(){
	return this.top;
}
```

Push is inputting a new node to the top node, overriding it. The algo is placing the previous top node to the next of the new top node. But if the nodes are still empty, then the top and bottom node is the same value.
```js
push(value){
	const newNode = new Node(value);
	if(!this.top){
		this.top = newNode;
		this.bottom = newNode;
	}
	else{
		let placeholder = this.top;
		this.top = newNode;
		this.top.next = placeholder;
	}
	this.length++;
	return this;
}
```

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}
```

The pop value is simple reoverring the newNode by the prev top node. But if the length becomes zero, bottom and top would be all null. 
```js
  pop() {
    this.length--;
    if(this.length > 0){
      this.top = this.top.next;
      return this;
    }

    else if(this.length == 0){
      this.bottom = null;
      this.top = null;
      return this;
    }
}
```


## Arrays

Implementing [[Stacks]] using [[Array Data Structure]] is relatively simpler. We just initialize an array like this
```js
class Stack {
  constructor() {
    this.array = [];
  }
}
```

Now, peek will look at the latest value which is the last index-value of the array
```js
peek(){
	return this.array[this.array.length - 1];
}
```

Push will add values to the end of array and we already have a builtin method for that
```js
push(value){
	this.array.push(value);
	return this;
}
```

Pop will remvoe values to the end of array
```js
pop(){
	this.array.pop();
	return this;
}
```


# Metatags
###### Related: [[Stacks]]
###### Tags: 
###### Source: 

---