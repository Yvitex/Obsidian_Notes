# Boiler plate
This is what the starting code of the framework looks like. 
First is we import the [[React]] library.
```js
import * as React from "react";
```

Next is to import the [[React Native]] specific library. This will consist of specific components needed to import by universal operator or just import it individually for a better performance
```js
import {Text, View, StyleSheet} from "react-native";
```

Just like in a normal [[React]] web application, we must have a app component that will export all the code in default
```js
import * as React from "react";
import {Text, View, StyleSheet} from "react-native";

export default function app(){
	return ();
}
```

Next is to write some native components we imported from the [[React Native]] library
```js
import * as React from "react";
import {Text, View, StyleSheet} from "react-native";

export default function app(){
	return (
		<View>
			<Text>Hello People</Text>
		</View>
	);
}
```

One thing to notice here is that <View /> element translates to <div /> element as said in [[React Native]] section and <Text /> translates to <p />. They are similar but convertible to both [[Android Architecture|android]] and ios.

![[Pasted image 20220718083534.png]]


Now to fix this up, we apply a styling using objects and StyleSheet native component. We do this by calling the [[StyleSheet]] then `.create()` method
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


![[Pasted image 20220718083827.png]]

One special property to include about styling is the property of flex, 
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
		flex: 1,
		paddingTop: 50,
		paddingLeft: 10,
	}
})
```