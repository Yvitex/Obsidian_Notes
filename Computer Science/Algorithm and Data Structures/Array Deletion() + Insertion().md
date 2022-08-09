# Deletion and Inserion
I already combined this two because there are pretty much the same in logic. They both have a time complexity of [[Linear  Time Complexity|O(n)]] as when an item is inserted or deleted, the other array element needs to adjust in order to occupy the spaces. We could demonstrate it using [[Javascript Splice]]

```js
let strings = ['a', 'b', 'c', 'd']

strings.splice(2, 0, "Ningen") // O(n)
```
![[Pasted image 20220802052608.png]]


[[Array Push() + Pop()]] is also a way to do delete and insert but in this case, it is more similar to Shift and Unshift

Unshift and shift
```js
strings.unshift("Z") //O(n)
```
![[Pasted image 20220802050909.png]]

and then
```js
strings.shift() //O(n)
```

We are actually making a [[Linear  Time Complexity|O(n)]] complexity in which we move all elements in an array forward from their original index and insert an element in the first index,Therefore it needs to loop through the length of an array. The same goes from [[Javascript Splice]].