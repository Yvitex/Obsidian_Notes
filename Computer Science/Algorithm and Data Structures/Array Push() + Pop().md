# Push/Pop
```js
let strings = ['a', 'b', 'c', 'd']
```

We could push()
```js
strings.push('e') // O(1)
```

![[Pasted image 20220802050336.png]]

Or pop()
```js
strings.pop() // O(1)
```
![[Pasted image 20220802050434.png]]

Both of this have a time complexity of [[Constant Time|O(1)]] as they are just adding some data at the end of the array. 
But it also could be [[Linear  Time Complexity|O(n)]] when it comes to [[Dynamic Arrays]]
