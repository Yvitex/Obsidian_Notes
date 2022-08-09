# Filter Search
We could use a [[Javascript Scpecial Operations]] to filter items into specific things
![[chrome-capture-2022-6-24.gif]]

If we want this kind of feature and we could revert back, then we need to save the original [[Data Structure]] and only modify something else. 

Here. we could use the [[Class Component Local State]] to do the job

```jsx
class App extends Component{
	constructor(){
		super();
		this.state = {
			monsters: []
		}
	}

	componentDidMount(){
		fetch("https://jsonplaceholder.typicode.com/users")
		.then((response) => response.json())
		.then((data) => this.setState(
			() => {
				return {monster : data}
			}))
	}

	render(){
		return <div>
					<input 
						className="search-box"
						type="search"
						placeholder="Search Monster"
						onChange={
							(event) => {
							
							}
						}
					/>
					{this.state.monsters.map((monster) => {
						return <h1>{monster.name}</h1>
					})}	
				</div>
	}
}
```

We created an [[Input Element]] that will act as our search box. As we type some text. the program will filter the content, We could do this using onChange method

First is convert it to lower case so that i could match easily with other values
```jsx
<input 
	className="search-box"
	type="search"
	placeholder="Search Monster"
	onChange={
		(event) => {
			let value = event.target.value.toLowerCase(); // convert to lower case			
		}
	}
```

Use the [[Javascript Scpecial Operations]] called filter. What we'ss filter is the state using the value
```jsx
<input 
	className="search-box"
	type="search"
	placeholder="Search Monster"
	onChange={
		(event) => {
			let value = event.target.value.toLowerCase(); // convert to lower case
			this.state.monsters.filter((monster) => {
				let filteredMonster = monster.name.toLowerCase();
				console.log(filteredMonster.includes(value));
				return filteredMonster.includes(value);
			})			
		}
	}
```

[[Javascript Includes]] returns true when the string have the specified characters
![[Pasted image 20220724104003.png]]

As we could see, when we search, we matched a single name from the array. The problem is that when we filter it and save it to the state component, what will happen is that we will override the previously fetched data from the [[API]]

What we could do is just create an external variable that will be mapped to the h1 [[HTML]] element
```jsx
render(){

	let filteredContent = this.state.monsters.filter((monster) => {
		let filteredMonster = monster.name.toLowerCase();
		console.log(filteredMonster.includes(value));
		return filteredMonster.includes(value);

	return (<div>
	<input 
		className="search-box"
		type="search"
		placeholder="Search Monster"
		onChange={
			(event) => {
				let value = event.target.value.toLowerCase(); // convert to lower case
				})			
			}
		}
	/>
	{this.state.monsters.map((monster) => {
		return <h1>{monster.name}</h1>
	})}	
	</div>);
	}
```

We set the filtered content to the filteredContent variable. The problem now is that we don't have access tot he  `event.target.value` value let alone the value variable. What we coudl do is to create another state or global variable that the outer function could access
```jsx
this.state = {
	monsters: [],
	filterer: ''
}
```

Then call the `setState`
```jsx
render(){

	let filteredContent = this.state.monsters.filter((monster) => {
		let filteredMonster = monster.name.toLowerCase();
		console.log(filteredMonster.includes(value));
		return filteredMonster.includes(value);

	return (<div>
	<input 
		className="search-box"
		type="search"
		placeholder="Search Monster"
		onChange={
			(event) => {
				let value = event.target.value.toLowerCase(); // convert to lower case
				this.setState(() => {
					return {filterer: value}
				})
				})			
			}
		}
	/>
	{this.state.monsters.map((monster) => {
		return <h1>{monster.name}</h1>
	})}	
	</div>);
	}
```

Next is to change the arguments in the `includes()` method
```jsx
render(){

	let filteredContent = this.state.monsters.filter((monster) => {
		let filteredMonster = monster.name.toLowerCase();
		console.log(filteredMonster.includes(this.state.filterer)); // debugging purpose
		return filteredMonster.includes(this.state.filterer); // change to state variable

	return (<div>
	<input 
		className="search-box"
		type="search"
		placeholder="Search Monster"
		onChange={
			(event) => {
				let value = event.target.value.toLowerCase(); // convert to lower case
				this.setState(() => {
					return {filterer: value}
				})
			})			
			
		}
	/>
	{this.state.monsters.map((monster) => {
		return <h1>{monster.name}</h1>
	})}	
	</div>);
	}
```

Now we could [[Javascript Scpecial Operations|map]] it out like before
```jsx
class App extends Component{
	constructor(){
		super();
		this.state = {
			monsters: [], 
			filterer: ''
		}
	}

	componentDidMount(){
		fetch("https://jsonplaceholder.typicode.com/users")
		.then((response) => response.json())
		.then((data) => this.setState(
			() => {
				return {monster : data}
			}))
	}

	render(){

	let filteredContent = this.state.monsters.filter((monster) => {
		let filteredMonster = monster.name.toLowerCase();
		console.log(filteredMonster.includes(this.state.filterer)); // debugging purpose
		return filteredMonster.includes(this.state.filterer); // change to state variable

	return (<div>
	<input 
		className="search-box"
		type="search"
		placeholder="Search Monster"
		onChange={
			(event) => {
				let value = event.target.value.toLowerCase(); // convert to lower case
				this.setState(() => {
					return {filterer: value}
				})
			})			
			
		}
	/>
	{filteredContent.map((monster) => { // changed from state variable to filteredContent
		return <h1>{monster.name}</h1>
	})}	
	</div>);
	}
}
```

This will still [[Rerender Class Component||rerender]] as when onChange Occurs, we call the `setState` method that triggers rerender everytime we make a change in the search bar. 

We could optimize if further by understanding the [[Anonymous Function Optimization]] and [[Destructuring]]

In destructuring, rather than calling the [[Java OOP Methods|this keyword]] multiple times, we could [[Destructuring|destructure]] the object
```jsx
render(){

	let {monsters, filterer} = this.state; // destructuring

	let filteredContent = this.state.monsters.filter((monster) => {
		let filteredMonster = monster.name.toLowerCase();
		console.log(filteredMonster.includes(filterer)); 
		return filteredMonster.includes(filterer); 
	return (<div>
	<input 
		className="search-box"
		type="search"
		placeholder="Search Monster"
		onChange={
			(event) => {
				let value = event.target.value.toLowerCase(); 
				this.setState(() => {
					return {filterer: value}
				})
			})			
			
		}
	/>
	{filteredContent.map((monster) => { 
		return <h1>{monster.name}</h1>
	})}	
	</div>);
}
```

We could also make the anonymous function in on change as a named function
```jsx
searchMonster = (event) => {
	let value = event.target.value.toLowerCase(); 
	this.setState(() => {
	return {filterer: value}
	})
})	
```

We could then lessen the return syntax
```jsx
render(){

	let {monsters, filterer} = this.state; // destructuring
	let {searchMonster} = this;

	let filteredContent = this.state.monsters.filter((monster) => {
		let filteredMonster = monster.name.toLowerCase();
		console.log(filteredMonster.includes(filterer)); 
		return filteredMonster.includes(filterer); 
	return (<div>
	<input 
		className="search-box"
		type="search"
		placeholder="Search Monster"
		onChange={searchMonster}
	/>
	{filteredContent.map((monster) => { 
		return <h1>{monster.name}</h1>
	})}	
	</div>);
}
```

