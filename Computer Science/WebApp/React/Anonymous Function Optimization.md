# Anonymous function vs Named function
One disadvantage of anonymous funciton pose on the program is that it is initiated at start up, and when there is 2 anonymous function of the same [[Algorithm]], then it is already redundant unlike named function we could use again and again. It is initiated twice or trice, depending on the number of anonymous funciton.

Using named function, we could initiate once, and run twice or trice. It is a more optimized way of doing it,

So when we are working with [[JS and HTML Events]], instead of using anonymous funciton, it is preferravle to use named function, or function declaration. 
```jsx
function clickEvent(){
	console.log("something");
}

return <button onClick={clickEvent}>Click</button>
```
