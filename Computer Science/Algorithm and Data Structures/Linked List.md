# Linked List
Are list that are linked. One node points to another node and it has a tail and a head where the tails points into null. 

![[Pasted image 20220807045945.png]]


Here is a website playground for [linked list](https://visualgo.net/en/list)

The main different between this [[Data Structure]] over the [[Array Data Structure]] is that this linked list is scattered all over the memory and it have no indexes so therefore there is no way to access it but through counting each item in a loop creating an [[Linear  Time Complexity|O(n)]]. The advantage of this is that it doesn't overflow? And also it doesn;t need to shift the rest of the items when inserting and deleting new items. 

The main advantage of this compared to [[Hash Table]] is that it is linked at has an order.

| Operation | Time Complexity |
| --------- | --------------- |
| Prepend   |      [[Constant Time\|O(1)]]           |
| Append    |   [[Constant Time\|O(1)]]                |
| Lookup    |   [[Linear  Time Complexity\|O(n)]]              |
| Delete    |   [[Linear  Time Complexity\|O(n)]]              |
| Insert          |  [[Linear  Time Complexity\|O(n)]]               |
