# Hash Table
This is one of the most common solution to optimize the [[Big O Asymptotic Analysis|time complexity]] from [[Quadratic Time|O(n^2)]] to much simpler ones. But this will result into a trade off between [[Space Complexity]] and [[Big O Asymptotic Analysis|time complexity]] where in because we improce the runtime, we will occupy more space. 

Hash table is simply a  [[Javascript Object]]. a [[Python Dictionary]]. It has different names from different languages but it is simply a key value pair enclosed inside a curly braces.

```js
let obj = {
	key: "value"
}
```

It is stored in the memory using a [[Hashing Function]] that convert the name into [[Memory address]]
Hashing function [[Big O Asymptotic Analysis|time complexity]] is [[Constant Time|O(1)]] as they happen really really fast. Some more mdoern [[Hashing Function]] takes a lot of time like in [[Cryptography]] but in our case, it is [[Constant Time]]. 

| Methods | Time Complexity |
| ------- | --------------- |
| [[Hashmap Insertion\|Insert]]  |    [[Constant Time\|O(1)]]             |
| [[Hashmap Lookup\|Lookup]]  |      [[Constant Time\|O(1)]]    or [[Linear  Time Complexity\|O(n)]]         |
| [[Hashmap Delete\|Delete]]  |      [[Constant Time\|O(1)]]             |
| [[Hashmap Search\|Search]]        |     [[Constant Time\|O(1)]]              |


Because hashing function is very fast, it will only have a constant time in any method... except if there is a [[Hash Collision]] which might make the look up turn into a [[Linear  Time Complexity]]. And also there is no concept of order meaning it is stored all over the place, unlike [[Array Data Structure]] and as we already knew, the closer the [[Memory address]] are to each other, they faster they to access the other. To make hash table completely hast, it needs a good collision resolution.

Hashtable is also called Associative [[Array Data Structure|arrays]] according to [wikipedia](https://en.wikipedia.org/wiki/Comparison_of_programming_languages_(associative_array))

We could also [[Construct Hashtable]]

## Problems
- [First Recurring Character](https://replit.com/@aneagoie/firstRecurringCharacter-exercise)
- 