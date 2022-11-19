---
aliases: [FIFO]
---
# Queues
This is like a line of person in the entrace of a movie. We add person on the last of the line, but we remove people who arrived first. 
![[Pasted image 20220929050337.png]]

First In First Out, FIFO, and that is a queue.
These are constucted in several apps, like hotel reservation, uber driver who first person who requested are entertained first. Like [[Stacks]]s it has the following operation:

| Operation | Time Complexity                   |
| --------- | --------------------------------- |
| Lookup    | [[Linear  Time Complexity\|O(n)]] |
| Enqueue   | [[Constant Time\|O(1)]]           |
| Dequeue   | [[Constant Time\|O(1)]]           |
| Peek      | [[Constant Time\|O(1)]]                                  |

Queues are built on top of [[Singly Linked List]] as we are in need for a fast deletion of first inserted items. We don't do [[Array Data Structure]] coz removing the first item will cause a [[Linear  Time Complexity]]. 


# Metatags
###### Related: [[Data Structure]], [[Stacks]]
###### Tags: 
###### Source: 

---