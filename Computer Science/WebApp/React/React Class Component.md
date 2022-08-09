# React
So far, we are commonly using what we call [[React Component|functional component]]in [[React]]. But we could also use class component, the syntax is as follows
```js
import React from "react";

class App extends React.Component{

}
```

In this case, we are inheriting from the `React.Component`. Then to return the jsx elements
```js
import React from "react";

class App extends React.Component{
	render(){
		return <h1>Hello World</h1>
	}
}
```

We need to call the render method and inside was to return the [[HTML]] element. 

We often use class component in the past because of its ability to update things
```js
import React from "react";

class ClassComponent extends React.Component {
	constructor() {
		super();
		this.state = {
		count: 0
	};
	
	this.increase = this.increase.bind(this);
}

increase() {
	this.setState({ count: this.state.count + 1 });
}

render() {
	return (
		<div>
			<h1>{this.state.count}</h1>
			<button onClick={this.increase}>+</button>
		</div>
	);
	}
}

export default ClassComponent;
```

But because we already have [[Hooks]] then maybe we don;t need this type of syntax. But for some sanity's sake, we could see how to change state by using [[Class Component Local State]]
