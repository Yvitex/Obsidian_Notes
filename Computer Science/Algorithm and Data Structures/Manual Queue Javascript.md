---
aliases: []
---
# Manual Queue Javascript
This is like how we built the [[Manual Stack Javascript]] using [[Singly Linked List]]
First create the constructor which will contain the length, the first and the last tracker but unlike the [[Stacks]]. the first variable will track the first inputted value and the last will track the latest inputted value.

```js
class Queue {
  constructor(){
    this.first = null;
    this.last = null;
    this.length = 0;
  }
}
```

Peek will output the first value we installed
```js
peek(){
	return this.first;
}
```

Enqueue will go to the next pointer of the latest node then update the last node with the newNode. If length is 0, then the first and last value are the same.
```js
enqueue(value){
	const newNode = new Node(value);
    if(this.length == 0){
      this.first = newNode;
      this.last = this.first;
    }
    else{
      this.last.next = newNode;
      this.last = newNode;
    }
    this.length++;
    return this;
}
```

dequeue wil delete the first variable through overriding like whatw e did with [[Manual Stack Javascript]].
```js
dequeue(){
	this.length--;
    if(this.length == 0){
      this.first = null;
      this.last = null;
      return this;
    }
    else{
      this.first = this.first.next;
      return this;
    }
}
```



# Metatags
###### Related: [[Queue]]
###### Tags: 
###### Source: 

---