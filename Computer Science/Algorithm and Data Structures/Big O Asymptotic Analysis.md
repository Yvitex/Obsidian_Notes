---
aliases: [Time Complexity]
---
# Big O 
Is a way to measure the [[Runtime]] or performance of a program by counting its operation. Each operation takes time  and using this analysis method, we could measure how good our code is. if it is a [[Good Code]] or a Bad Code.

## Measures or Time Complexity
- [[Linear  Time Complexity]]
- [[Constant Time]]
- [[Quadratic Time]]
- [[Factorial Time]]
- [[Logarithmic Time Complexity]]
- [[Exponential Time Complexity]]
- [[Loglinear Time Complexity]]

In analysis, we need to ming the[[Big O Reading Rules]]

## Challenge
What do you think is the Big O of this algorithm

```js
function funChallenge(input) {
  let a = 10; 
  a = 50 + 3; 

  for (let i = 0; i < input.length; i++) { 
    anotherFunction(); 
    let stranger = true; 
    a++; 
  }
  return a; 
}
```

3 of the operation run on once and 4 of them is inside a loop. Therefore, Big O(3 + 4n) or simply O(n)

```js
function anotherFunChallenge(input) {
  let a = 5; // O(1)
  let b = 10; // O(1)
  let c = 50; // O(1)
  for (let i = 0; i < input; i++) { // O(n)
    let x = i + 1; // O(n)
    let y = i + 2; // O(n)
    let z = i + 3; // O(n)

  }
  for (let j = 0; j < input; j++) { // O(n)
    let p = j * 2; // O(n)
    let q = j * 2; // O(n)
  }
  let whoAmI = "I don't know"; // O(1)
}
```

It is O(4 + 7n) but to simplify, we could just use O(n)

[[Big O Asymptotic Analysis]]

Why do we need to know about this??
Simply it makes us aware that we have hoe infinite resources. For example, instead of running a loop to find the last and the first part of an array, we would just imply choose a call property like array\[0]
 and array\[array.length - 1]
 ```js
 "ajdahdenansdandw".length
```

The above function also, we could be aware of the language. We could look up and search if the method we are using has has a [[Big O Asymptotic Analysis|time complexity]] of O(n) or O(1), In this case, because in [[Javascript]] it is a property of an object then it is only O(1) which is great.



![[5.1 BigO-cheat-sheet (1).pdf.pdf]]

 ## Big O Case Ranges
 
![[Pasted image 20220731051420.png]]

