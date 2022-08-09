# Space Complexity
There are 2 ways a program could store data... the [[Heap]] and the [[Stack]]
Sometimes. when space complexity increase, the [[Big O Asymptotic Analysis|time complexity]] decrease. 

What causes some Space Complexity are:
- Variables - well obviously
- [[Data Structure]]
- [[Function Call]]
- [[Allocations]]


```js
function boooo(n) {
    for (let i = 0; i < n; i++) {
        console.log('booooo');
    }
}
```

We also use [[Big O Asymptotic Analysis]] to identify the [[Scalability]] of the storage space,  In the function above, we only created one variable inside the for loop therefore the space complexity above is O(1)

```js
function arrayOfHiNTimes(n) {
    var hiArray = [];
    for (let i = 0; i < n; i++) {
        hiArray[i] = 'hi';
    }
    return hiArray;
}
```

In this function, we are creating a new [[Data Structure]] called an array. Each item we insert inside an array takes space and because it is based on a loop then the space complexity would be O(n)




