# TRicks
Basically a way to create a switching page automatically depending on the state or [[Hooks]] in a both [[React]] or [[React Native]]. We could event apply it to the [[Embedded Javascript Templating|ejs]] principle

First is to create a basic [[React Native Boiler Plate]]
```js
import * as React from "react";
import {Text, View, StyleSheet} from "react-native";

export default function app(){
	return (
		<View style={style.components}>
			<Text>Hello People</Text>
		</View>
	);
}

const style = StyleSheet.create({
	components: {
		paddingTop: 50,
		paddingLeft: 10,
	}
})
```

Create a [[Hooks]]
```js
import React, {useState} from "react";
import {Text, View, StyleSheet} from "react-native";

export default function app(){
	const [focusSubject, setFocus] = useState(null);

	return (
		<View style={style.components}>
			<Text>Hello People</Text>
		</View>
	);
}

const style = StyleSheet.create({
	components: {
		paddingTop: 50,
		paddingLeft: 10,
	}
})
```

Create a [[Conditional Rendering]] based on those [[Hooks]]
```js
import React, {useState} from "react";
import {Text, View, StyleSheet} from "react-native";

export default function app(){
	const [focusSubject, setFocus] = useState(null);

	return (
		<View style={style.components}>
			{focusSubject ? <Text>Have state</Text> : <Text>No State</Text>}
		</View>
	);
}

const style = StyleSheet.create({
	components: {
		paddingTop: 50,
		paddingLeft: 10,
	}
})
```

![[Pasted image 20220718091506.png]]

Replace the Text with a [[React Native Component]] page. 
