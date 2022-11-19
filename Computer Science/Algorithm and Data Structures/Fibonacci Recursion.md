---
aliases: []
---
# Fibonacci Recursion
We will solve for the fibonacci using a given indes. Fibonacci is a sequence of number that was generated in terms of its previous number
`0, 1, 1, 2, 3, 5, 8, 13, 21, 34`

Recursive solution:
```js
function fibonacciRecursive(n) {
  if (n < 2) {
    return n
  }
  return fibonacciRecursive(n - 1) + fibonacciRecursive(n-2)
}
```

What's going on here, our base case is simply 0 or 1 which is equal to their indices. We will return then the sum of the fibonacci of the previous number before it. 

Iterative Solution:
```js
function fibonacciIterative(n) {
  let start = 0;
  let step = 1;
  let result = 0
  for (let i = 1; i < n; i++) {
    result = start + step;
    start = step;
    step = result
  }
  return result;
}
```

Here we create a for loop that will assign and reassign the number sequence until it hits a dead end. Else, we could use an array:
```js
function fibonacciIterative(n) {
  let result = [0, 1];
  for(let i = 1; i < n; i++){
    result.push(result[i - 1] + result[i])
  }
  return result[n];
}
```

We are simply adding the 2 first values in the array then return the specified indes. 

The lesson here is that the [[Recursion]] could be a lot worser than iteration, because what we did in this fibonacci problem is this.  ![[Pasted image 20221006050615.png]]

We are calling fibonacci twice and it grows overtime like a tree. The [[Big O Asymptotic Analysis|time complexity]] is [[Exponential Time Complexity|O(2 ^ n)]]. While the iterative solution is [[Linear  Time Complexity|O(n)]]. [[Exponential Time Complexity]] is a lot worse than [[Linear  Time Complexity]] which is why when we crank up the n value of the function above in the recursion, it is very slow because it is doing thousands or more calculation. For example, we have 30 as n, then the iterations happening under the hood is 2 ^ 30 which is 1,073,741,824 calculation. 

# Metatags
###### Related:[[Recursion]]
###### Tags: #problem 
###### Source: 

---