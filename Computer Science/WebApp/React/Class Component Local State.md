# Class Component
We knew how to construct a class, in this section, we will teach you how to use states to have a similar effect as using [[Hooks]] in [[React]]

```js
import { Component } from "react";

class App extends Component(){

	render(){
		return (
	    <div className="App">
	      <header className="App-header">
	        <img src={logo} className="App-logo" alt="logo" />
	        <p>
	          Welcome Yvitex
	        </p>	
	        <button>Slap Er Butt</button>	
	        <a	
	          className="App-link"
	          href="https://reactjs.org"
	          target="_blank"	
	          rel="noopener noreferrer">	
	          Learn React
	        </a>
	      </header>
	    </div>
	  );
	}
}
```

This is some basic boiler plate using [[React Class Component]]. It looks like this
![[Pasted image 20220723103505.png]]

Will change the name Yvitex to something else, with some [[Conditional Rendering]] and other tricks. It might be harder to command the [[React]] application to [[Rerender Class Component]]. For example, we could make the name dynamic by using a constructor. 
```js
import { Component } from "react";

class App extends Component(){
	constructor(){
	super();
	
	}

	render(){
		return (
	    <div className="App">
	      <header className="App-header">
	        <img src={logo} className="App-logo" alt="logo" />
	        <p>
	          Welcome Yvitex
	        </p>	
	        <button>Slap Er Butt</button>	
	        <a	
	          className="App-link"
	          href="https://reactjs.org"
	          target="_blank"	
	          rel="noopener noreferrer">	
	          Learn React
	        </a>
	      </header>
	    </div>
	  );
	}
}
```

With this, we could set an object that will hold into the state, we use the name `state` as the variable in which [[React]] will look for. And also use [[Java OOP Methods|this keyword]] as we are inside a class component
```js
import { Component } from "react";

class App extends Component(){
	constructor(){
	super();

	this.state = {
		name: "Yvitex"
	}
	}

	render(){
		return (
	    <div className="App">
	      <header className="App-header">
	        <img src={logo} className="App-logo" alt="logo" />
	        <p>
	          Welcome {this.state.name}}
	        </p>	
	        <button>Slap Er Butt</button>	
	        <a	
	          className="App-link"
	          href="https://reactjs.org"
	          target="_blank"	
	          rel="noopener noreferrer">	
	          Learn React
	        </a>
	      </header>
	    </div>
	  );
	}
}
```

When we command the button to change the state through a function like this.
```jsx
r But<button onClick = {() => this.state.name = "Goshujin-sama"}>Slap Et</button>	
```

```ad-Danger
title: Error, it does not render!!!
collapse: open
If we try and click this, it still the same. But when we console log it, we could see that the value has changed
WHYYYYY
```

This will not work, why? [[React]] only rerenders when it detects a change in the entire object, meaning even though we change the value of that object, it is still the same object, it is still the same [[Memory address]]. Look further into this topic at [[Javascript Objects Equality]]

What we could do is to use the [[React]] method called `setState` to make the [[DOM]] [[Rerender Class Component]]
```jsx
<button onClick = {() => this.setState({name: "Goshujin-sama"}) = "Goshujin-sama"}>Slap Er Butt</button>
```

This is actually called [[Shallow merge]]

To wrap things up:
```jsx
import { Component } from "react";

class App extends Component(){
	constructor(){
	super();

	this.state = {
		name: "Yvitex"
	}
	}

	render(){
		return (
	    <div className="App">
	      <header className="App-header">
	        <img src={logo} className="App-logo" alt="logo" />
	        <p>
			 {this.state.name == "Goshujin-sama" && "Nyaa!"} Welcome {this.state.name}
	        </p>	
			<button onClick = {() => this.setState({name: "Goshujin-sama"})}>Slap Er Butt</button>
	        <a	
	          className="App-link"
	          href="https://reactjs.org"
	          target="_blank"	
	          rel="noopener noreferrer">	
	          Learn React
	        </a>
	      </header>
	    </div>
	  );
	}
}
```

![[chrome-capture-2022-6-23.gif]]

![[5gqaat.gif]]


```ad-note
collapse: open
The author does not mean to sexualize any women. Just imagine it as a guy dressed in a maid uniform. And no, I'm not gay

```

One thing to notice about this code is that when we console log it on click
```jsx
<button onClick = {() => 
			this.setState({name: "Goshujin-sama"};
			console.log(this.state);
			}>Slap Er Butt</button>
```

![[chrome-capture-2022-6-23 (1).gif]]

We could see that it doesn't really update on the first click though we could see that the changes are rendered inside the viewport. WHY? This could be explained by the concept of [[Synchronous programming]] and [[Asynchronous programming]]

`this.setState` runs asynchronous to other processes and `console.log` runs synchronous. The simplest explanation is that despite we declare that `console.log()` should run after we set the states, [[React]] first executes it before executing `setState`.  To prevent this, the most optimate way to write a `setState` function is to create a callback function
```jsx
<button
	onClick={() => {
		this.setState(() => {return {name: "Goshujin-sama"},
		() => { console.log(this.state) };
	);
}
}>Slap Er Butt </button>
```

This will accept 2 parameters, first is the return statement, and next is what do after the execution. 
This also have 2 parameters
```jsx
this.setState((state, props) => {})
```

state contains all previous satte and props contains the [[React Properties]]
