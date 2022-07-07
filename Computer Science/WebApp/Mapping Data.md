# Mapping Data
In our past lesson in [[Atomic React]], we provided a code that is pretty hardcoded. [[React]]
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

We could see that we could use a for loop in this kind of equation, but it is... hard in terms when using react so here we use a method called `[[Javascript Scpecial Operations|map]]`

We will map the imported contacts to our liking
```js
contacts.map()
```

[[Javascript Scpecial Operations|Map]] will accept a parameter function, where this function will return the component that makes up the card. The parameter we will use inside the funciton will contain each and individual peace of our data from contact.
```js
function contactList(contact){
	return <Card
		name={contact.name}
		img={contact.imgURL}
		tel={contact.phone}
		email={contact.email}
	/>
}
```

We do not need to use an index as map method will already scan the array of object for us automatically.
```js
contacts.map(contactList)
```

This will cause an error to the console. We need to specify a unique identification for each of our individual card component 
```js
function contactList(contact){
	return <Card
		key={contact.id}
		name={contact.name}
		img={contact.imgURL}
		tel={contact.phone}
		email={contact.email}
	/>
}
```

OVerall
```js
import React from "react";
import Card from "./Card";
import contacts from "../contacts";

function contactList(contact){
	return <Card 
			key={contact.id}
			name={contact.name}
			img={contact.imgURL}
			tel={contact.phone}
			email={contact.email}
			/>
}

function App() {
return (
	<div>
		<h1 className="heading">My Contacts</h1>
		contacts.map(contactList)
	</div>

);

}

export default App;
```

We create a map method for the imported array, the value extracted from the array will be passed as the parameter of the parameter of the function we passed in the map, each value will be called individuall as a return value. 

For more info. read [[Javascript Scpecial Operations]]