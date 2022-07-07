# Conditional Rendering in React
How can we render something when a condition is true and render another different thing when the codition is false. 
```js
import React from "react";
function App() {

return (
	<div className="container">
		<h1>Hello</h1>
		<form className="form">
		<input type="text" placeholder="Username" />
		input type="password" placeholder="Password" />
		<button type="submit">Login</button>
		</form>
	</div>
);
}

export default App;
```

We could simply create a function with an if else statement inside. Here, we create another component container that will isolate the login component to improve readability
```js
import React from "react";

function conditionalRendering(){
	if(isLoggedIn){
		return <h1>Hello</h1>
	}
	else{
		return <Login />
	}
}

function App() {
let isLoggedIn = true;

// then we can call it inside the returned value

return (
	<div className="container">
	{conditionalRendering()}
	</div>
);
}

export default App;
```

The easier way is to create a ternary expression, we can't do in if, else statement directly inside jsx as it is only available for [[React Expression]]

```js
import React from "react";

function App() {
let isLoggedIn = true;

// then we can call it inside the returned value

return (
	<div className="container">
	{isLoggedIn ? <h1>Hello</h1> : <Login /> }
	</div>
);
}

export default App;
```

If we only  have to render 1 thing, when true it will render, when false it will not render anything at all, then we could use the `&&` operator

```js
import React from "react";

function App() {
let isLoggedIn = true;

// then we can call it inside the returned value

return (
	<div className="container">
	{isLoggedIn && <h1>Hello</h1> }
	</div>
);
}

export default App;
```

When isLoggedIn is true, we render the h1 element, if not, we render nothing.


This form of conditioning is called [[Declarative Programming vs Imperative Programming|declarative programming]] where the state of the component is dependent upon the state of a variable, namely `isLoggedIn`
