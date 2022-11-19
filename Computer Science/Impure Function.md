---
aliases: []
---
Impure functions are functions that may output something different in the same argument
```js
let c = 2;
function impure(a, b){
	return a + b + c;
}
```

There is one variable that is not stated in the function, the c. Becayse this variable may change and is not controlled by the arguments of the function, then it is an impure function.

For example, a is 1 and b is 1, the output is 4 and will be 4. But we may accidentally change c to equals 4. This could then output 6 rather than 4.

Impure functions like this could also cause a [[Function SideEffect]]


# Metatags
###### Related: [[Pure Functions]]
###### Tags: 
###### Source: 

---