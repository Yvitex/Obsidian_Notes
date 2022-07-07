# React Properties
In [[React Component]]. For an instance that there are repeated items in the code, though with different headings, or other properties. We could simplify it by creating a property aka props that will create a dynamic setting for us to input some differences in the item. Simply, inside the function we pass a name as a parameter `function Name(props)`. So basically this is a callback function where all the string data or other value are stored

In the renderer, we could do it like this
```js
ReactDOM.render( <div>
				<h1>My Contacts</h1>
				<Card 
					name = "Kei"
					image = "https://64.media.tumblr.com/a8e2bd20069091562fb159763f36414c/tumblr_pq4p36hOlK1ubc65j_1280.jpg"
					tel = "+123 456 789"
					mail = "idunno@mail.com"	
				/>
				</div>, document.getElmenetById("root"))
```

We could create imaginary properties where we identidy the string or value of something. Behind the scenes, we do some stuff in a [[React Component]]


```js
import React from "react";
import ReactDOM from "react-dom";

function Card(props){
	return <div>
				<h1>{props.name}</h1>
				<img src={props.image} alt="avatar_img" />
				<p>{props.tel}</p>
				<p>{props.mail}</p>
		   </div>
}
```

We treat `props` like a [[Javascript]] object called with a dot syntax followed by the name of the imaginary attributes we created in the renderer. This will set the values of the component according to what we passed inside the renderer.  This makes the component reusable. 

```js
import React from "react";
import ReactDOM from "react-dom";

function Card(props) {
return (
<div>
<h2>{props.name}</h2>
<img src={props.image} alt="avatar_img" />
<p>{props.tel}</p>
<p>{props.mail}</p>
</div>
);
}
  
ReactDOM.render(
<div>
<h1>My Contacts</h1>

<Card
name="Kei"
image="https://64.media.tumblr.com/a8e2bd20069091562fb159763f36414c/tumblr_pq4p36hOlK1ubc65j_1280.jpg"
tel="+123 456 789"
mail="idunno@mail.com"
/>

<Card
name="Sakayanagi"
image="https://pbs.twimg.com/media/E4raElbXoAYgt3t.jpg"
tel="+123 666 221"
mail="sakayanagi@class.com"

/>

<Card
name="Naoko"
image="https://i.pinimg.com/736x/61/02/46/610246c40c5c947760099b411c19d7dd.jpg"
tel="666"
mail="pumpkinpie143@inhellbitch.com"

/>

</div>,

document.getElementById("root")

);
```

![[Pasted image 20220627172249.png]]


