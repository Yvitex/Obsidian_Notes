# Shallow Merge
Is different between the context of vanilla [[Javascript]] and [[React]]

In react, a shallow merge is defined as the overriding of values when properties of an object matches even though the complexity of that object is different. For example

```jsx
class App extends Component(){
	constructor(){
	super();

	this.state = {
		name: {firstName: "Yvitex", lastName: "Chuuni"}
	}
	}

	render(){
		return (
	    <div className="App">
			<p>{this.state.name.firstName} {this.state.name.lastName}</p>
			<button onClick = {() => {this.setState({name: "Yvi"})}}>click</button>
	    </div>
	  );
	}
}
```

This will render nothing when the button is pressed. It is because we modify the [[Data Structure]] object from `name: {firstName: "Yvitex", lastName: "Chuuni"}` to `name: "Yvi"` which will cause a bug when we call it to the renderer as `this.state.name.firstName` because `state.name` is not a complex object anymore.
In summary, shallow merge is just a merge in shallow tone. It will only updates shallowly anything that matches the specified property and not the deeper properties.