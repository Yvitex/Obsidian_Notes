# Linked List
Are list that are linked. One node points to another node and it has a tail and a head where the tails points into null. 

![[Pasted image 20220807045945.png]]


Here is a website playground for [linked list](https://visualgo.net/en/list)

The main different between this [[Data Structure]] over the [[Array Data Structure]] is that this linked list is scattered all over the memory and it have no indexes so therefore there is no way to access it but through counting each item in a loop creating an [[Linear  Time Complexity|O(n)]]. The advantage of this is that it doesn't overflow? And also it doesn;t need to shift the rest of the items when inserting and deleting new items. 

We have another type of linked list called [[Doubly Linked List]], and the advantage of singly was it occupies less memory and it is easier to implement. 

The main advantage of this compared to [[Hash Table]] is that it is linked at has an order.

| Operation | Time Complexity                   |
| --------- | --------------------------------- |
| Prepend   | [[Constant Time\|O(1)]]           |
| Append    | [[Constant Time\|O(1)]]           |
| Lookup    | [[Linear  Time Complexity\|O(n)]] |
| Delete    | [[Linear  Time Complexity\|O(n)]] |
| Insert    | [[Linear  Time Complexity\|O(n)]] |


We could now then create a [[Manual Javascript Singly Linked List]]

Now why use linked list, we could optimzie deletions of element (push and pop) in a [[Hash Table]] in the context where items suffer from [[Hash Collision]]. This type of [[Data Structure]] too is similar to how the file syste in our computer works where we could go to the next and previous. Unlike [[Hash Table]] it has an order, and it is much more flexible in size compared to [[Static Arrays]]. It also have faster insertion and deletion compared to [[Array Data Structure]] coz once they have the reference, it will just delete it and done, arrays will have to shift everything back and forth. 

The problems in linked list is that there is a slow lookup and occupies more memory due to frequent use of [[Reference Type]] and creation of objects.



