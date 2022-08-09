# React Native Component
To create a react native component, it is the same way we create in [[React Component]]

Here is the basic code from [[Navigation Tricks]]
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

What we will do, is that when the [[Hooks]] is null, we will render a react native component page. Create a new folder in the src/feature/ called focus and create a new js file called focus
![[Pasted image 20220718092708.png]]

Inside this focus file, write the [[React Native Boiler Plate]], clean the parts and rename the functional component as `Focus()` in which we will export using named function, read why in [[Named Export vs Export default]]
```js
import React from 'react';
import { Text, View, StyleSheet } from 'react-native';

export const Focus = () => {
  return (
    <View style={styles.component}>
      <Text> Rendering none </Text>
    </View>
  );
}
```

We will move the styling in this file, we will only need the `flex` property and some background styling in the app component
```js
import React from 'react';
import { Text, View, StyleSheet } from 'react-native';

export const Focus = () => {
  return (
    <View style={styles.component}>
      <Text> Rendering none </Text>
    </View>
  );
}

const styles = StyleSheet.create({
	component: {
		flex: 1,
	    paddingTop: 50,
	}
})
```

In the main app component, we import it like this.
```js
import React, {useState} from "react";
import {Text, View, StyleSheet} from "react-native";
import {Focus} from "./src/features/Focus/Focus"

export default function app(){
	const [focusSubject, setFocus] = useState(null);

	return (
		<View style={style.components}>
			{focusSubject ? <Text>Have state</Text> : <Focus />}
		</View>
	);
}

const style = StyleSheet.create({
	components: {
		flex: 1,
		background: "aqua",
	}
})
```
![[Pasted image 20220718093239.png]]
