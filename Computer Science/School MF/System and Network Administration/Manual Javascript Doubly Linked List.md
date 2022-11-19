---
aliases: []
---
# Manual Javascript Doubly Linked List
We could simply take the code from the [[Manual Javascript Singly Linked List]]
```js
class LinkedList {
  constructor(value) {
    this.head = {
      value: value,
      next: null
    };
    this.tail = this.head;
    this.length = 1;
  }
  append(value) {
    const newNode = {
      value: value,
      next: null
    }
    this.tail.next = newNode;
    this.tail = newNode;
    this.length++;
    return this;
  }
  prepend(value) {
    const newNode = {
      value: value,
      next: null
    }
    newNode.next = this.head;
    this.head = newNode;
    this.length++;
    return this;
  }
  printList() {
    const array = [];
    let currentNode = this.head;
    while(currentNode !== null){
        array.push(currentNode.value)
        currentNode = currentNode.next
    }
    return array;
  }
  insert(index, value){
    //Check for proper parameters;
    if(index >= this.length) {
      console.log('yes')
      return this.append(value);
    }
    
    const newNode = {
      value: value,
      next: null
    }
    const leader = this.traverseToIndex(index-1);
    const holdingPointer = leader.next;
    leader.next = newNode;
    newNode.next = holdingPointer;
    this.length++;
    return this.printList();
  }
  traverseToIndex(index) {
    //Check parameters
    let counter = 0;
    let currentNode = this.head;
    while(counter !== index){
      currentNode = currentNode.next;
      counter++;
    }
    return currentNode;
  }
  remove(index) {
    // Check Parameters      
    const leader = this.traverseToIndex(index-1);
    const unwantedNode = leader.next;
    leader.next = unwantedNode.next;
    this.length--;
    return this.printList();
  }
}
```

In the constructor, create a new part of the object named previous
```js
constructor(value) {
    this.head = {
      value: value,
      next: null,
      previous: null,
    };
    this.tail = this.head;
    this.length = 1;
  }
```

Next, in the append method, we will simply do the same an assign the previous value to that object property
```js
append(value) {
    const newNode = {
      value: value,
      next: null,
      previous: null,
    }
    newNode.previous = this.tail;
    this.tail.next = newNode;
    this.tail = newNode;
    this.length++;
    return this.tail;
  }
```

Next is the prepend method, we do the same, and assign null to the new Node, set the previous head node with previous assigned to the new node
```js
prepend(value) {
    const newNode = {
      value: value,
      next: null,
      previous: null,
    }
    this.head.previous = newNode;
    newNode.next = this.head;
    this.head = newNode;
    this.length++;
    return this.tail;
  }
```

To manually insert element using an index, add the previous, set the new node's previous into the leader, we get the leader by traversing into index - 1 which is the previous value before index. The next next value will then have the previous value pointing to the newNode. 
```js
insert(index, value) {
    //Check for proper parameters;
    if (index >= this.length) {
      console.log('yes')
      return this.append(value);
    }

    const newNode = {
      value: value,
      next: null,
      previous: null,
    }
    const leader = this.traverseToIndex(index - 1);
    newNode.previous = leader;
    const holdingPointer = leader.next;
    holdingPointer.previous = newNode;
    leader.next = newNode;
    newNode.next = holdingPointer;
    this.length++;
    return this.printList();
  }
  traverseToIndex(index) {
    //Check parameters
    let counter = 0;
    let currentNode = this.head;
    while (counter !== index) {
      currentNode = currentNode.next;
      counter++;
    }
    return currentNode;
  }
```

To remove element using index, we will get simply the next next node after the leader and then apply a previous value to it which points to the leader. Change also the leader's next to the value of he next next node.
```js
remove(index) {
    // Check Parameters      
    const leader = this.traverseToIndex(index - 1);
    const unwantedNode = leader.next;
    const nextToUnwanted = unwantedNode.next
    leader.next = unwantedNode.next;
    nextToUnwanted.previous = leader
    this.length--;
    return this.printList();
  }
```











# Metatags
###### Related: [[Manual Javascript Singly Linked List]]
###### Tags: 
###### Source: 

---