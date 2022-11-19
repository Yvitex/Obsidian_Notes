---
aliases: []
---
# Manual Binary Search Tree Javascript
[[Binary Search Tree]] have 3 functionalitues, the lookup, the insertion and deletion. 
Here we first create a node creator with 3 different properties and they are the pointer to the right, left and the node value.
```js
class Node {
  constructor(value) {
    this.left = null;
    this.right = null;
    this.value = value;
  }
}
```

Now for the actual [[Data Structure]], create a class with a constructr for the root that for now, equals to 1.
```js
class BinarySearchTree {
  constructor() {
    this.root = null;
  }
}
```

Insertion method will use [[Reference Type|Pointer]] just like [[Singly Linked List]]. The [[Algorithm]] will set the root into the new node when the root is null, else we will create a while loop that will check weather the newNode's value is less than or greater than the root and we will decide then where to go, was it to set the newNode to the right of the root? to the left? or just to traverse to the right and check the current node again, here is the code. 
```js
insert(value) {
    const newNode = new Node(value); // new node
    if (!this.root) {
      this.root = newNode; // set the new node to root if root is null
    }
    else {
      let temp = this.root; // store the root to a temporary pointer
      while (temp) {
        if (newNode.value < temp.value) {
          if (!temp.left) { // if the left of the temporary pointer is null, 
            temp.left = newNode; // assign the new node to the left
            break; // exit the loop
          }
          else {
            temp = temp.left; // if the left of temp pointer is not null, update the temp with it
          }
        }
        else if (newNode.value > temp.value) {
          if (!temp.right) {
            temp.right = newNode;
            break;
          }
          else {
            temp = temp.right;
          }
        }
      }
    }
  }
```

In look up we will use the same algoritm
```js
lookup(value) {
    let temp = this.root;
    let step = 0;
    while(temp){
      step++; // track the height of the BST
      if (value < temp.value){
        if(temp.left){
          temp = temp.left;
        }
        else{
          return false; // return false and break loop once it can't proceed
        }
      }
      else if(value > temp.value){
        if(temp.right){
          temp = temp.right;
        }
        else{
          return false;
        }
      }
      else if(value == temp.value){
        console.log(value + " in step: " + step); // if the value is equal to a node, yey. 
        break; // break the loop
      }
    }
  }
```

To delete in BST, this is very hard but here is the code which i didn't create
```js
remove(value) {
    if (!this.root) {
      return false;
    }
    let currentNode = this.root;
    let parentNode = null;
    while(currentNode){
      if(value < currentNode.value){
        parentNode = currentNode;
        currentNode = currentNode.left;
      } else if(value > currentNode.value){
        parentNode = currentNode;
        currentNode = currentNode.right;
      } else if (currentNode.value === value) {
        //We have a match, get to work!
        
        //Option 1: No right child: 
        if (currentNode.right === null) {
          if (parentNode === null) {
            this.root = currentNode.left;
          } else {
            
            //if parent > current value, make current left child a child of parent
            if(currentNode.value < parentNode.value) {
              parentNode.left = currentNode.left;
            
            //if parent < current value, make left child a right child of parent
            } else if(currentNode.value > parentNode.value) {
              parentNode.right = currentNode.left;
            }
          }
        
        //Option 2: Right child which doesnt have a left child
        } else if (currentNode.right.left === null) {
          currentNode.right.left = currentNode.left;
          if(parentNode === null) {
            this.root = currentNode.right;
          } else {
            
            //if parent > current, make right child of the left the parent
            if(currentNode.value < parentNode.value) {
              parentNode.left = currentNode.right;
            
            //if parent < current, make right child a right child of the parent
            } else if (currentNode.value > parentNode.value) {
              parentNode.right = currentNode.right;
            }
          }
        
        //Option 3: Right child that has a left child
        } else {

          //find the Right child's left most child
          let leftmost = currentNode.right.left;
          let leftmostParent = currentNode.right;
          while(leftmost.left !== null) {
            leftmostParent = leftmost;
            leftmost = leftmost.left;
          }
          
          //Parent's left subtree is now leftmost's right subtree
          leftmostParent.left = leftmost.right;
          leftmost.left = currentNode.left;
          leftmost.right = currentNode.right;

          if(parentNode === null) {
            this.root = leftmost;
          } else {
            if(currentNode.value < parentNode.value) {
              parentNode.left = leftmost;
            } else if(currentNode.value > parentNode.value) {
              parentNode.right = leftmost;
            }
          }
        }
      return true;
      }
    }
  }
```

I don't know yet how this works, but I'll gonna do my own soon. 






# Metatags
###### Related: 
###### Tags: 
###### Source: 

---