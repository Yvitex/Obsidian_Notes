# Events
There are different events we could choose inside [[HTML]], the only thing you must remember is that in [[Javascript]], we must change the case of their names. For example, onclick must be onClick on javascript or [[React]]'s jsx

The most common event is the `onClick` event, we use a function that will execute when we click a certain element, heavily used in [[Hooks]]
```js
import React, {useState} from "react";
function App(){

let [initial, setInitial] = useState("");

function changeExecute(){
	setInitial("Hello World")
}

return  <div>
			<h1>{initial}</h1>
			<button onClick={changeExecute}>Click</button>
		</div>
}
```

Next one is `onMouseOver` and `onMouseOut`, we could use it to change the background color or others but it is more efficient to do this on CSS
```js
import React, {useState} from "react";
function App(){

let [initial, setInitial] = useState("white");

function mouseEnter(){
	setInitial("black");
}

function mouseLeave(){
	setInitial("white")
}

return  <div>
			<h1>{initial}</h1>
			<button 
				style={{backgroundColor: initial} 
				onMouseOver={mouseEnter}
				onMouseOut={mouseLeave}
			>
			>Click</button>
		</div>
}
```


We could also use `onChange()` method. In this case, we use event callback inside the function to be executed

```js
import React, {useState} from "react";
function App(){

let [initial, setInitial] = useState("");

function userIsTyping(event){
	setInitial(event.target.value);
}

return  <div>
			<h1>Hello {initial}</h1>
			<input 
				type="text"
				placeholder="Enter your name"
				onChange={userIsTyping}
			/>
			<button>Click</button>
		</div>
}
```

Though this is on its incomplete form, inside a form component, inputs, text area and select must be controlled as the changes in their value is not recorded in [[React]] unlike ordinary [[HTML]]. So what we will going to do is that we will **store the text we made to the value component**. Simply
```js
import React, {useState} from "react";
function App(){

let [initial, setInitial] = useState("");

function userIsTyping(event){
	setInitial(event.target.value);
}

return  <div>
			<form>
			<h1>Hello {initial}</h1>
			<input 
				type="text"
				placeholder="Enter your name"
				onChange={userIsTyping}
				value={initial}
			/>
			<button type="submit">Click</button>
			</form>
		</div>
}
```

Another useful method to consider is `event.preventDefault()`, in a form that you don;t need to submit a request, we could use this to prevent reload

```js
import React, {useState} from "react";
function App(){

let [initial, setInitial] = useState("");
let [heading, setHeading] = useState("");

function userIsTyping(event){
	setInitial(event.target.value);
}

function clickButton(event){
	setHeading(initial);
	event.preventDefault();
}

return  <div>
			<form onSubmit={clickButton}>
			<h1>Hello {heading}</h1>
			<input 
				type="text"
				placeholder="Enter your name"
				onChange={userIsTyping}
				value={initial}
			/>
			<button type="submit">Click</button>
			</form>
		</div>
}
```

So what we have done here is to change the h1 element only if we click the button, we set the value of initial to the function changer of heading, but when we click the button it will reload making our effor bootless. What we do is to create a callback event then use it to call `preventDefault()`.

I am lazy, here's all the [documentation](https://www.w3schools.com/tags/ref_eventattributes.asp) for all the events we could use![[girl-anime.gif]]
