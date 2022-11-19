# Hooks
[[React]] have its own renderer which makes it hard to make changes to the interface of the website dynamically. Using hooks, we make it possible. We utilize the ability of hooks by importing the `useState` class

Hooks allow us to control when the website render or re render.

```js
import React, {useState} from "react";
```

`useState` is not a default import. We could read more in [[Importing in Javascript]]
Next is we use the value of useState and store it inside a [[Destructuring]] variables. Tjis will return a value and a function. `useState` will accept the initial value as an argument.

```js
import React, {useState} from "react"

function App(){
	const [count, setCount] = useState(0);
}
```

If we are using buttons, such as

```js
import React, {useState} from "react"

function App(){
	const [count, setCount] = useState(0);


	return (
		<div>
			<h1>0</h1>
			<button>+</button>
		</div>
	);
}
```

We could create a function and use the `onClick` attribute to call that function. Hardcoded 0 must be replaced by the dunamic value fromt he destructured components. We also use the `setCount` function
```js
import React, {useState} from "react"

function App(){
	const [count, setCount] = useState(0);

	function increase(){
		setCount(count + 1);
	}

	return (
		<div>
			<h1>{count}</h1>
			<button onClick={increase}>+</button>
		</div>
	);
}
```

Adding more functionalities
```js
import React, {useState} from "react"

function App(){
	const [count, setCount] = useState(0);

	function increase(){
		setCount(count + 1);
	}

	function decrease(){
		setCount(count - 1);
	}

	return (
		<div>
			<h1>{count}</h1>
			<button onClick={increase}>+</button>
			<button onClick={decrease}>+</button>
		</div>
	);
}
```

![[chrome-capture-2022-6-3.gif]]

