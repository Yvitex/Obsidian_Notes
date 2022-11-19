---
aliases: []
---

# React Component
There are 2 types of component and they are [[React Class Component]] and [[React Functional Component]]

```js
import React from "react";
import ReactDOM from "react-dom"; 

ReactDOM.render(
<div>
	<h1>My Favourite Foods</h1>
	<ul>
		<li>Bacon</li>
		<li>Jamon</li>
		<li>Noodles</li>
	</ul>
</div>,document.getElementById("root")
);
```

[[React]] could separate this into small individual components. Doing this pose a lot of benefits
- It will become more readable. It is said that the longer the code is, the less understable it is.
- Modular, can be reused

To separate it, we create a function with a name starting with a **Capital Letter**. Inside it will return a html code we wanted to render. 

```js
function Heading(){
	return <h1>My Favourite Foods</h1>
}
```

We will render it as an [[HTML]] element in a format of a self closing html element
```js
import React from "react";
import ReactDOM from "react-dom"; 

function Heading(){
	return <h1>My Favourite Foods</h1>
}


ReactDOM.render(
<div>
	<Heading />
	<ul>
		<li>Bacon</li>
		<li>Jamon</li>
		<li>Noodles</li>
	</ul>
</div>,document.getElementById("root")
);
```

It is a convention to space the name to the closing tag. In the end it will render the same

![[Pasted image 20220627061131.png]]

Next step is to create a file called Heading.jsx. It is a jsx extension which is why the file name extension is different. Also we prefer to use capitalized title. 
Inside here, we will copy our function, import react and export function. 
```js
# inside Heading.jsx
import React from 'react';

function Heading(){
	return <h1>My Favourite Foods</h1>
}

export default Heading;
```

Inside the main [[Javascript]] file, we import the heading file.
```js
import React from "react";
import ReactDOM from "react-dom"; 
import Heading from "./Heading";

function Heading(){
	return <h1>My Favourite Foods</h1>
}

ReactDOM.render(
<div>
	<Heading />
	<ul>
		<li>Bacon</li>
		<li>Jamon</li>
		<li>Noodles</li>
	</ul>
</div>, document.getElementById("root")
);
```

## Bonus
To return a multiple componnent in a single function
```js
function List(){
	return (
		<ul>
			<li>Bacon</li>
			<li>Jamon</li>
			<li>Noodles</li>
		</ul>
		);
}

export default List;
```

In multiple components, we do not directly import it to the main [[Javascript]] file but instead, we create another jsx called *App.jsx* to compile every components. 
```js
import List from "./List"
import Heading from "./Heading"
import React from "React"

function App(){
	return <div>
			<Heading />
			<List />	
		   </div>
}

export default App
```

The we import this app component to the main file renderer

```js
import React from "react";
import ReactDOM from "react-dom"; 
import App from "./App"

ReactDOM.render(<App />,document.getElementById("root")
);
```

```ad-Attention
title: Components, components
collapse: open
We always store each and every components withing the component folder so instead of using the file path "./Component" we actually use ./"components, Component"

```

```js
import React from "react";
import ReactDOM from "react-dom"; 
import App from "./components/App"

ReactDOM.render(<App />,document.getElementById("root")
);
```

Maybe you don;t know the art of [[Importing in Javascript]], read it here. 
