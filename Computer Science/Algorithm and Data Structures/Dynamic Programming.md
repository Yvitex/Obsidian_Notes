---
aliases: []
---
# Dynamic Programming
The name dynamic programming came from the programmer's butt. This concept is actually all about [[CPU Cache|cache]] and using this to speed up our program by storing data in to the [[CPU Cache|cache]].

An important topic of DP is called [[Memoization]] which is a specific form of storing data into the [[CPU Cache|cache]]
In actuality, DP is all about [[Divide and Conquer]] plus [[Memoization]]. For example, when solving [[Fibonacci Recursion]] problem, we could actually improve upon it to emlimate some other calculations though we are trading some [[Space Complexity]] in order to reduce the [[Big O Asymptotic Analysis|Time Complexity]] from [[Exponential Time Complexity]] to [[Linear  Time Complexity]].

So in our [[Fibonacci Recursion]] problem, we could add a [[CPU Cache|cache]] mechanism to improve this:
```js
function fibonacciMemo(){
  const cache = {}
}
```

Now return the recursive function, check weather the function already exist inside the cache and return it, else, calculate it using recursion and then push it to the [[CPU Cache|cache]]. 
```js
function fibonacciMemo(){
  const cache = {}
  return function fibonacciRecursive(n){
    if(n in cache){
      return cache[n];
    }
    else{
      if(n < 2){
        cache[n] = n;
        return cache[n]
      }
      else{
        cache[n] = fibonacciRecursive(n - 1) +   fibonacciRecursive(n - 2);
        return cache[n]
      }
    }
  }
}
```

This transform our [[Quadratic Time|O(n^2)]] to [[Linear  Time Complexity|O(n)]]
![[Pasted image 20221012152501.png]]

We could apply dynamic programming if they are comply to
- Can be use [[Divide and Conquer]]
- [[Recursion]] or recursive solution
- Repetivie subproblem
- [[Memoization|memoiz]] subproblem


# Metatags
###### Related: 
###### Tags: 
###### Source: 

---