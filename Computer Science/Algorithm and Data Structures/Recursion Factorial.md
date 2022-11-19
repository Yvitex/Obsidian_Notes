---
aliases: []
---
# Factorial
Solve factorial in 2 different ways, first is through the use of [[Recursion]], second is through loops

Factorial solusion:
```js
function findFactorialRecursive(number) {
  if (number == 0){ // conditional check
  	return 0
  }
  else if (number == 1) {
    return 1
  }
  let answer = number * findFactorialRecursive(number - 1);
  return answer
}
```

The factorial solution is formatted like this, (n * !(n - 1)). When number is equal to 1, then we return one to complete the base case. We then return the multiplication of all the returned number.  

Loop solution:
```js
function findFactorialIterative(number) {
  let answer = 1;
  for(let i = number; i > 1; i--){
    answer *= i;
  }
  return answer;
}
```

In the loop solution, we will simply accumulate the produc of number that decrements. Both of these solutions are [[Linear  Time Complexity|O(n)]]

# Metatags
###### Related: [[Recursion]]
###### Tags: #problem 
###### Source: 

---