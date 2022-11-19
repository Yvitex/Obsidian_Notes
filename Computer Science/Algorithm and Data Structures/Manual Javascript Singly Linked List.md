---
aliases: []
---
# Manual Javascript Linked List
In [[Javascript]], the code that will represent the linked list of values with 10 > 5 > 16 is something that look like this
```js
const linkedList = {
	head: {
		value: 10,
		next: {
			value: 5,
			next: {
				value: 16,
				next: null
			}
		}
	}
}
```

The object ofcourse will have a head, a head is a node that is a container of 2 values which is the current value and then the  next node that will contain another value. 
So to create our own class for linked list we have to do this:

Create a class, this will have an initial value that will be our head value
```js
class LinkedList{
	constructor(initialValue){
		this.head = {
			value: initialValue,
		}
	}
}
```

This head node will reference to the next node and because we don't have a current next node value, then we apply a null that completes temporarily our linked list
```js
class LinkedList{
	constructor(initialValue){
		this.head = {
			value: initialValue,
			next: null,
		}
	}
}
```

Of course because this is the only value we have, the tail will also be the same as the head, add the length which is 1
```js
class LinkedList{
	constructor(initialValue){
		this.head = {
			value: initialValue,
			next: null,
		}
		this.tail = this.head;
		this.length = 1;
	}
}

LinkedList(10);
```

For now, the linked list that we have is a 10 ---> null. Now we create the following functionality

## Append

We will add values to the end of the linked list so that it will form something like this 10 --> 5 --> 16. And to do that, we will take advantage in the concept of [[Reference Type]] or [[Reference Type|Pointer]]s. We will create a new node, and for that node, we will get the last item, and make the node's next value points to the new node. Increment the length
```js
append(value){
	this.length++;
	const newNode = {
		value: value,
		next: null
	}
}
```

We wull then update the whole linked list by finding the last item in the `this.tail`, get the next and refer it to the new node
```js
append(value){
	const newNode = {
		value: value,
		next: null
	}
	this.tail.next = newNode;
}
```

We update then the last tail to be that new node
```js
append(value){
	const newNode = {
		value: value,
		next: null
	}
	this.tail.next = newNode;
	this.tail = newNode;
}
```

```js
let myLinkedList = new LinkedList(10);
console.log(myLinkedList.append(5));
console.log(myLinkedList.append(16));
```

Output:
{ value: 10, next: { value: 5, next: { value: 16, next: null } } }

## Prepend

Adding an item at the beginning of the linked list is easy. Create a new node, and make the next key inside that node refer to the current head node. We will then update the current headnode to be that new node. Increment the length

```js
prepend(value){
	this.length++;
	const newNode = {
		value: value,
		next: null
	}
	newNode.next = this.head;
	this.head = newNode;
	return this.head; 
}
```

```js
let myLinkedList = new LinkedList(10);
console.log(myLinkedList.append(5));
console.log(myLinkedList.append(16));
console.log(myLinkedList.prepend(2));
console.log(myLinkedList.prepend(8))
```

Output:
{ value: 8, next: { value: 2, next: { value: 10, next: \[Object] } } }

Because, we are using the newNode variable repeatedly, we could create a new class just for it
```js
class Node{
  constructor(value){
    this.value = value;
    this.next = null;
  }
}
```


## Traverse

We could do the rest of the oepration having [[Linear  Time Complexity]]. We will use a while loop in order to print all values as an array. We create a container, get the currentNode which is the head node, when currentNode is not yet null, push the value to the container and then update the currentNode tot he nextNode.

```js
printAsArray(){
	const array = [];
	let currentNode = this.head;
    while(currentNode !=  null){
      array.push(currentNode.value);
      currentNode = currentNode.next;
    }
    return array;
  }
}
```

## Insert

To insert a value in the specific index, we will use a loop once again
```js
insert(index, value){

}
```

The first thing we need to do is to check the index, if it is 0, prepend, if equal or greater than the length, append
```js
insert(index, value){
    if(index >= this.length){
      this.append(value)
    }
    else if(index == 0){
      this.prepend(value)
    }
}
```

If not, we will create a for loop that will traverse the linked list nested objects depending on the index. We use here index -1 because our target is the previous value, so if we have 10 -> 11 ->14 -> 34. If we have index of 2. we will try to get 11 because we want to modify its next value. Before that, create a new storage node, also. get the current node
```js
insert(index, value){
    if(index >= this.length){
      this.append(value)
    }
    else if(index == 0){
      this.prepend(value)
    }
    let currentNode = this.head;
    const newNode = new Node(value);
    for(let i; i < index - 1; i++){
	    currentNode = currentNode.next;
    }
}
```

Now, we want to first store to a temporary variable the value of the next value of the current node. We will assign a new next value to it then we will apply the termporary variable as the next value of that new next value
So if we have: 10 -> 11 ->14 -> 34, we want to insert 23 at index 2 will get 11, we store 14 -> 34 -> null to a temp variable, we set the 11's next value as the new node which is 23 -> null, we replace then the null with temp variable which is 14 -> 34

```js
insert(index, value){
    if(index >= this.length){
      this.append(value)
    }
    else if(index == 0){
      this.prepend(value)
    }
    let currentNode = this.head;
    const newNode = new Node(value);
    for(let i; i < index - 1; i++){
	    currentNode = currentNode.next;
    }
    let temp = currentNode.next
    currentNode.next = newNode
    newNode.next = temp
    return this
}
```

We could separate the loop to a different method
```js
insert(index, value){
	if(index >= this.length){
	  this.append(value)
	}
	else if(index == 0){
	  this.prepend(value)
	}
	else{
	  let currentNode = this.head;
	  const newNode = new Node(value);
		
	  currentNode = this.traverseLinkedList(index, currentNode)
		
	  let temp = currentNode.next
	  currentNode.next = newNode
	  newNode.next = temp
	  return this
	}
}

traverseLinkedList(index, currentNode){
	for(let i = 0; i < index -1 ; i++){
	  currentNode = currentNode.next
	}
	return currentNode;
}
```

## Remove

Will simply use the traverseLinkedList to traverse in the objects, if index == 0, then we simply override the this.head with the next value. Else, we are going to use the traversal function to get the current node and override it with its next value
```js
remove(index){
	let currentNode = this.head;
	this.length--;
	if(index == 0){
	  currentNode = currentNode.next
	  this.head = currentNode
	  return this
	}
	else{
	  currentNode = this.traverseLinkedList(index, currentNode);
	  currentNode.next = currentNode.next.next
	  return this 
	}
}
```

# Metatags
###### Related: [[Singly Linked List]], [[Reference Type]], [[Garbage Collection]]
###### Tags: #
###### Source: 

---


```js
class LinkedList{
	constructor(value){
		this.head = {
			value: value,
			next: null
		}
		this.tail = this.head;
		this.length = 1;
	}
	append(value){
		const newNode = {
			value: value,
			next: null
		}

		this.tail.next = newNode;
		this.tail = newNode;
		return this.head;
	}
	
	prepend(value){
		this.length++;
		const newNode = {
			value: value,
			next: null
		}
		newNode.next = this.head;
		this.head = newNode;
		return this.head; 
	}

}
```