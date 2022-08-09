# How to control parent component from child?
If you are confused, just imagine this
![[Pasted image 20220707110734.png]]

We have this program, when we cick on the list, it deletes. butthe component list is separated from the data array in another [[React Component]].
```js
import React from 'react';

function ToDoList(props){
	return <li>{props.list}</li>
}
export default ToDoList;
```

This is the component we have. In another jsx app file, we have this
```js
<ul>
	{items.map((items) => (
		<ToDoList
		list={items}
	/>
	))}
</ul>
```

The [[Data Structure]] `items` is an array where we map it to print each list inside the untitled list. To delete an item fromt he first component, then we need a function to aid the process
```js
function deleteItem(){
	
}
```

Then we pass this as a parameter to the component jsx.
```js
<ul>
	{items.map((items) => (
		<ToDoList
		list={items}
		handleClick={deleteItem}
	/>
	))}
</ul>
```

Inside our component jsx. We could create an [[JS and HTML Events|event]] where we will pass this parameter function, see [[React Properties]]

```js
import React from 'react';

function ToDoList(props){
	return <li onClick={props.handleClick} >{props.list}</li>
}
export default ToDoList;
```

But we need to be specific what items we need to delete depending on the item we click, So therefore we need to create a way to identify the items. Inside the app component, we will pass an id and key. Also `map` method have a parameter called index. See [[Javascript Scpecial Operations]]
```js
<ul>
	{items.map((items, index) => (
		<ToDoList
		list={items}
		handleClick={deleteItem}
		key={index} //should not be because it needs to be unique
		id={index} // this is what we will pass as a parameter inside the function
	/>
	))}
</ul>
```

Indie our component, we will pass this id, to the function
```js
import React from 'react';

function ToDoList(props){
	return <li onClick={props.handleClick(props.id)} >{props.list}</li>
}
export default ToDoList;
```

```ad-Danger
title: Immediate execution!!
collapse: open
The problem is, this will immediately execute the function because we apply a () for the parameter, we could use a nested function for it. In our case, anonymous function for easier syntax

```

```js
import React from 'react';

function ToDoList(props){
	return <li onClick={() => {
		props.handleClick(props.id)
	}} >{props.list}</li>
}
export default ToDoList;
```

Then we will create a parameter inside app jsx that will catch this value
```js
function deleteItem(id){
	
}
```

Now we could create an actual functionality that will delete the item, in our case because we are in [[React]] then we are forced to use [[Hooks]].
First is we recollect the previous values available. 
```js
const [list, setList] = useState([]);

function deleteItem(id){
	setList((prev) =>{
		
	})
}
```

Then we will filter this out to remove only the element of an specific id. Also [[Javascript Scpecial Operations]]'s filter method have an index like map
```js
const [list, setList] = useState([]);

function deleteItem(id){
	setList((prev) =>{
		return prev.filter((item, index) => {
			return index != id;
		})
	})
}
```

```ad-Attention
title: Do not forget
collapse: open
Do not forget the return statement after each function we create.

```
