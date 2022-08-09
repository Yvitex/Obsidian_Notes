# React Hooks
A continuation from the lesson of [[Hooks]]. We could also create multiple hooks in a single object.

```js
import React, {useState} from "react";

function App(){


return (
	<div className="container">
		<h1>
		Hello {fullName.firstName} {fullName.lastName}
		</h1>
		<form>
			<input name="fName" placeholder="First Name" />
			<input name="lName" placeholder="Last Name" />
			<button>Submit</button>
		</form>
	</div>
	);
}

export default App;
```

How we do this is instead of
```js
let [firstName, setFirstName] = useState("");
let [lastName, setLastName] = useState("");
```

We do this
```js
let [fullName, setFullName] = useState({
	fName: "",
	lName: "",
});
```

We create an object as an argument.  Inside our input elements, what we will do is for every [[JS and HTML Events|onChange]] events, we will render or update the component. 
```js
import React, {useState} from "react";

function App(){

let [fullName, setFullName] = useState({
	fName: "",
	lName: "",
});

function handleChange(){
	
}

return (
	<div className="container">
		<h1>
		Hello {fullName.firstName} {fullName.lastName}
		</h1>
		<form>
			<input onChange={handleChange} name="fName" placeholder="First Name" />
			<input onChange={handleChange} name="lName" placeholder="Last Name" />
			<button>Submit</button>
		</form>
	</div>
	);
}

export default App;
```

Using ordinary means, when we try to types something isnide the input element, it will erase the value of another element. So what we will do is inside our function handler, we will update the object from its initial state using a function.
```js
function handleChange(){

	setFullName((prevValue) => {
		
	})
}
```

Depending on what component we will try to type in, the specified hook will render while we preserve the previous value of another. To do this, we need to tap in inside the `event.target.name` and also its value `event.target.value`
```js
function handleChange(event){

	let value = event.target.value;
	let name = event.target.name;

	setFullName((prevValue) => {
		if(name == "fName"){
			return{
				fName: value,
				lName: prevValue.lName
			}
		else if(name =="lName"){
			return{
				fName: prevValue.fName,
				lName: value
			}
		}
		}
	})
}
```

Now, to wrap things us, we need to fix the jsx [[HTML]] to become a controlled component
```js
import React, {useState} from "react";

function App(){

let [fullName, setFullName] = useState({
	fName: "",
	lName: "",
});

function handleChange(event){

	let value = event.target.value;
	let name = event.target.name;

	setFullName((prevValue) => {
		if(name == "fName"){
			return{
				fName: value,
				lName: prevValue.lName
			}
		else if(name =="lName"){
			return{
				fName: prevValue.fName,
				lName: value
			}
		}
		}
	});
}

return (
	<div className="container">
		<h1>
		Hello {fullName.fName} {fullName.lName}
		</h1>
		<form>
			<input 
				value={fullName.fName} 
				onChange={handleChange} 
				name="fName" 
				placeholder="First Name" 
			/>
			<input 
				value={fullName.lName}
				onChange={handleChange} 
				name="lName" 
				placeholder="Last Name" 
			/>
			<button>Submit</button>
		</form>
	</div>
	);
}

export default App;
```

![[747825f64867b7e4bc1a3771d3f5975f.gif]]

Too long and confusing for us  to understand MF, so to simplify this we use the art of [[Spread Operator]] and [[Destructuring]]

```js
function handleChange(event){

	let value = event.target.value;
	let name = event.target.name;

	setFullName((prevValue) => {
		if(name == "fName"){
			return{
				fName: value,
				lName: prevValue.lName
			}
		else if(name =="lName"){
			return{
				fName: prevValue.fName,
				lName: value
			}
		}
		}
	})
}
```

Now, to wrap things us, we need to fix the jsx [[HTML]] to become a controlled component
```js
import React, {useState} from "react";

function App(){

let [fullName, setFullName] = useState({
	fName: "",
	lName: "",
});

function handleChange(event){

	let value = event.target.value;
	let name = event.target.name;

	setFullName((prevValue) => {
		return{
		...prevValue,
		[name]: value
		}
	});
}

return (
	<div className="container">
		<h1>
		Hello {fullName.fName} {fullName.lName}
		</h1>
		<form>
			<input 
				value={fullName.fName} 
				onChange={handleChange} 
				name="fName" 
				placeholder="First Name" 
			/>
			<input 
				value={fullName.lName}
				onChange={handleChange} 
				name="lName" 
				placeholder="Last Name" 
			/>
			<button>Submit</button>
		</form>
	</div>
	);
}

export default App;
```

`[name]` is basically a shortcut to use a variable and not for [[Javascript]] to interpret it as a new keyword. `...prevValue` is just the key-value pair inside the prevValue callback extracted using [[Spread Operator]]


![[chrome-capture-2022-6-3(222).gif]]