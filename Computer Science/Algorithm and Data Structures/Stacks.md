---
aliases: [LIFO]
---
# Stacks
Are list plates in a stack, we shouldn't get the plate on the middle but rather we could remove the top plate one after another  until we reach our target plate. ![[Pasted image 20220929044418.png]]
We could only Grab and remove the top most input, which is the last or latest input. Last Input but First to get out, LIFO, Last in First out. 
We use stacks in many areas of programming, engines like in [[Javascript]] use stacks which is why we could sometimes encounter the error called [[Call Stack|Stack overflow]]. Undo and Redo functions are also like stacks, or any other functionalities where the last item we add appears first. 

| Operation | Time Complexity                   |
| --------- | --------------------------------- |
| Lookup    | [[Linear  Time Complexity\|O(n)]] |
| Push      | [[Constant Time\|O(1)]]           |
| Pop       | [[Constant Time\|O(1)]]           |
| Peek      | [[Constant Time\|O(1)]]           |

This have 4 operatiosn, push is to add another item to the last, pop is to delete the last item, peek is to view the last item and lookup was the very most inefficient functionality that let you traverse the stack.

Stacks are built on top of [[Array Data Structure]] because we need to delete or modify the last item in the collection. We could pull also this using [[Doubly Linked List]] but that's not good cause it will occupy a lot of memory coz we need to track a lot of pointers. Moreover, arrays have this [[Cache Locality]] where in it stores item in successive memory location therefore having faster access. 

# Metatags
###### Related: [[Data Structure]], [[Queue]]
###### Tags: 
###### Source: 

---

