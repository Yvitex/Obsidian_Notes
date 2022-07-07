---
aliases: [declarative programming, imperative programming]
---

# Declarative programming
A programmign where state of components are dependent upon the value of a variable, commonly a boolean

```js
let isLoggedIn = true;

function Component(){
return isLoggedIn ? <h1>Welcome</h1> : <h1>You must login first</h1>
}
```

# Imperative programming
Is when we access the component on a deeper level as such
```js
function strikethrough(){
	document.getElementById("root").style.textDecoration = "line-through";
}

function nostrikethrough(){
	document.getElementById("root").style.textDecoration = null;
}


function App(){
	return (<div>
			<p>Buy milk</p>
			<button onClick={strikethrough}>Change to strike through</button>
			<button onClick={nostrikethrough}>Change back</button>
		</div>);
}

```

![[Pasted image 20220630161638.png]]

This may change the satte of the component, but when we apply the same principle with declarative programming
```js

let isDone = false;

function strikethrough(){
	isDone = true;
}

function nostrikethrough(){
	isDone= false;
}


function App(){
	return (<div>
			<p style={isDone && {textDecoration: "line-through"}>Buy milk</p>
			<button onClick={strikethrough}>Change to strike through</button>
			<button onClick={nostrikethrough}>Change back</button>
		</div>);
}
```

Then this will not work. the button will not work because it is not being rendered in the virtual dom unlike accessing it in the htmp using imperative progrmaming. But there is a hope, we could use what the react people called [[Hooks]]

Related: [[React Expression]], [[Conditional Rendering]], [[React Styling]]