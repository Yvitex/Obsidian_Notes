# React
[[React]] is desigend to make your components reusable making the development easier. This lesson is an advance lesson for [[React Component]]s where we pass [[React Properties]] into different levels
```js
import React from "react";

function Card(props) {
return (
	<div className="card">
		<div className="top">
			<h2 className="name">{props.name}</h2>
			<img className="circle-img" src={props.img} alt="avatar_img" />
			</div>
			<div className="bottom">
			<p className="info">{props.tel}</p>
			<p className="info">{props.email}</p>
		</div>
	</div>
	);
}
  
export default Card;
```

In this code, we could make the image and the p element into a separate component, creating a 2 level deep component

We create a separate file for the image as in
```js
import React from "react"

function Avatar(props){
return <img className="circle-img" src={props.img} alt="avatar_img" />
}

export default Avatar;
```

We could see that the code above acceots a property named img,  In our Card component...
```js
import React from "react";
import Avatar from "./Avatar"

function Card(props) {
return (
	<div className="card">
		<div className="top">
			<h2 className="name">{props.name}</h2>
			<avatar img={props.img} />
			</div>
			<div className="bottom">
			<p className="info">{props.tel}</p>
			<p className="info">{props.email}</p>
		</div>
	</div>
	);
}
  
export default Card;
```

We could pass another property that will satisfy our property in Avatar component. This property will accept value from App component. We could do the same in our p element
```js
import React from "react"

function Detail(props){
return <p className="info">{props.info}</p>

}

export default Detail;
```

This will accept a property in the name of info, in our card component
```js
import React from "react";
import Avatar from "./Avatar"
import Detail from "./Detail"

function Card(props) {
return (
	<div className="card">
		<div className="top">
			<h2 className="name">{props.name}</h2>
			<avatar img={props.img} />
			</div>
			<div className="bottom">
			<Detail info={props.tel} />
			<Detail info={props.email} />
		</div>
	</div>
	);
}
  
export default Card;
```

This may be confusing bu [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en) extension for chrome might help.

Inside the App component, we could specify this like this
```js
import React from "react";
import Card from "./Card";
import contacts from "../contacts";

function App() {
return (
<div>
<h1 className="heading">My Contacts</h1>
  
<Card
name={contacts[0].name}
img={contacts[0].imgURL}
tel={contacts[0].phone}
email={contacts[0].email}
/>

<Card
name={contacts[1].name}
img={contacts[1].imgURL}
tel={contacts[1].phone}
email={contacts[1].email}
/>

<Card
name={contacts[2].name}
img={contacts[2].imgURL}
tel={contacts[2].phone}
email={contacts[2].email}
/>
</div>

);

}

export default App;
```

Where contact is an array of objects containing data
```js
const contacts = [
{
id: 1,
name: "Beyonce",
imgURL:
"https://blackhistorywall.files.wordpress.com/2010/02/picture-device-independent-bitmap-119.jpg",
phone: "+123 456 789",
email: "b@beyonce.com"
},
{
id: 2,
name: "Jack Bauer",
imgURL:
"https://pbs.twimg.com/profile_images/625247595825246208/X3XLea04_400x400.jpg",
phone: "+987 654 321",
email: "jack@nowhere.com"
},

{
id: 3,
name: "Chuck Norris",
imgURL:
"https://i.pinimg.com/originals/e3/94/47/e39447de921955826b1e498ccf9a39af.png",
phone: "+918 372 574",
email: "gmail@chucknorris.com"
}
];

export default contacts;
```
