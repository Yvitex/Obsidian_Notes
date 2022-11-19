---
aliases: []
---
# Reverse a Linked List
To reverse a [[Singly Linked List]] which does not have a previous pointer, we could do this

Set method
```js
reverse(){

}
```

Get the first 2 nodes
```js
reverse(){
	let first = this.head;
	let second = this.head.next;
}
```

Create a while loop that will reverse the [[Reference Type|Pointer]] reference while there is a second value. To do that, we first store the third value for later use
```js
reverse(){
	let first = this.head;
	let second = this.head.next;
	while(second){
		let temp = second.next;
	}
}
```

Next is to reverse the pointer
```js
reverse(){
	let first = this.head;
	let second = this.head.next;
	while(second){
		let temp = second.next;
		second.next = first;
	}
}
```

Update the 2 variables to switch to the new values
```js
reverse(){
	let first = this.head;
	let second = this.head.next;
	while(second){
		let temp = second.next;
		second.next = first;
		first = second;
		second = temp;
	}
}
```

Because the this.head will still refer to the previous this.head, we will update its next property pointing to null coz it is already the tail value 
```js
reverse(){
	let first = this.head;
	let second = this.head.next;
	while(second){
		let temp = second.next;
		second.next = first;
		first = second;
		second = temp;
	}
	this.head.next = null;
}
```

We will update the head to the previous tail stored in first variable
```js
reverse(){
	let first = this.head;
	let second = this.head.next;
	while(second){
		let temp = second.next;
		second.next = first;
		first = second;
		second = temp;
	}
	this.head.next = null;
	this.head = first;
}
```

Last thing is to update teh this.tail to the first previous value
```js
reverse(){
	let first = this.head;
	this.tail = first;
	let second = this.head.next;
	while(second){
		let temp = second.next;
		second.next = first;
		first = second;
		second = temp;
	}
	this.head.next = null;
	this.head = first;
}
```


# Metatags
###### Related: [[Singly Linked List]]
###### Tags: #problem
###### Source: 

---