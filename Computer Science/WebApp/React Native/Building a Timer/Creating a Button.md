# Button Creation
In creating button in [[React Native]], we use the component `TouchableOpacity`
```js
import React from 'react';
import { Text, StyleSheet, TouchableOpacity } from 'react-native';
```

Here is the documentation regarding [TouchableOpacity](https://reactnative.dev/docs/touchableopacity). It is just a button that when you click will fade. Still we need to style it to make it look like a button.

Now, create a function that will return something
```js
import React from 'react';
import { Text, StyleSheet, TouchableOpacity } from 'react-native';

export const RoundedButton = () => {
  return (
  ); 
}
```

We could then use this component. This is not an actual button but a container like div with an ability to be clicked.
```js
import React from 'react';
import { Text, StyleSheet, TouchableOpacity } from 'react-native';

export const RoundedButton = () => {
  return (
	 <TouchableOpacity>
     <Text></Text>
     </TouchableOpacity>
  ); 
}
```

We want this to be a recyclable component, we pass [[React Properties]], in this state, we could pass multiple [[React Properties]] as an object. We could even use a spread operator to make things more dynamic
```js
import React from 'react';
import { Text, StyleSheet, TouchableOpacity } from 'react-native';

export const RoundedButton = ({
	styles = {},
	size = 125,
	textStyle = {},
	...props
	}) => {
  return (
	 <TouchableOpacity>
     <Text></Text>
     </TouchableOpacity>
  ); 
}
```

This syntax is kinda strange, we use `=` rather than `:` in an object?
Next is that we need to apply them, passing multiple [[React Properties]] needs to be an array.
```js
import React from 'react';
import { Text, StyleSheet, TouchableOpacity } from 'react-native';

export const RoundedButton = ({
	styles = {},
	size = 125,
	textStyle = {},
	...props
	}) => {
  return (
	 <TouchableOpacity style={styles}>
     <Text style={textStyle}>{props.title}</Text>
     </TouchableOpacity>
  ); 
}
```

It is possible for `props.title` to be functional as we set `props` as a [[Spread Operator]]. Also, notice that the styling is null because, what we need to do is to pass some of this props to the [[StyleSheet]] and we could do that by assigning the variable as a function
```js
import React from 'react';
import { Text, StyleSheet, TouchableOpacity } from 'react-native';

export const RoundedButton = ({
	styles = {},
	size = 125,
	textStyle = {},
	...props
	}) => {
  return (
	 <TouchableOpacity style={styles}>
     <Text style={textStyle}>{props.title}</Text>
     </TouchableOpacity>
  ); 
}

const styles = (sizes) => StyleSheet.create({

})
```

This styling makes the function anabled to accept some properties from the function. To make the stling easier, go and import the function to the Focus component in [[Text Input and Styling]] section
```js
import React from 'react';
import { Text, View, StyleSheet } from 'react-native';
import {TextInput} from "react-native-paper";
import {RoundedButton} from "../../components/RoundedButton"

export const Focus = () => {
  return (
    <View style={styles.component}>
      <View style={styles.componentTitle}>
        <Text style={styles.titleText}>What would you like to focus on? </Text>
        <View style={styles.inputBox}>
          <TextInput />
          <RoundedButton title="+" />
        </View>
      </View>
    </View>
  );
}
```
![[Pasted image 20220718115913.png]]

We want this to be bigger.  Create some styling that will do this and apply it to the component in an array if multiple properties, the syntax should be `styles(sizes).something`  because it is a function we are working with
```js
import React from 'react';
import { Text, StyleSheet, TouchableOpacity } from 'react-native';

export const RoundedButton = ({
	styles = {},
	size = 125,
	textStyle = {},
	...props
	}) => {
  return (
	 <TouchableOpacity style={[styles, styles(size).radius]}>
     <Text style={textStyle}>{props.title}</Text>
     </TouchableOpacity>
  ); 
}

const styles = (sizes) => StyleSheet.create({
	radius: {
		borderColor: "white",
		borderWidth: 2,
		height: sizes,
		width: sizes,
	}
})
```
![[Pasted image 20220718120237.png]]

To fix this, use borderRadius, also apply appropriate properties for the text element
```js
import React from 'react';
import { Text, StyleSheet, TouchableOpacity } from 'react-native';

export const RoundedButton = ({
	styles = {},
	size = 125,
	textStyle = {},
	...props
	}) => {
  return (
	 <TouchableOpacity style={[styles, styles(size).radius]}>
     <Text style={[textStyle, styles(size).innerText]}>{props.title}</Text>
     </TouchableOpacity>
  ); 
}

const styles = (sizes) => StyleSheet.create({
	radius: {
		borderColor: "white",
		borderWidth: 2,
		height: sizes,
		width: sizes,
		borderRadius: sizes / 2,
	    alignItems: "center"
    },
    innerText: {
	    fontSize: sizes / 2,
	    marginTop: "10%",
	    color: "white"
	}
})
```

![[Pasted image 20220718121111.png]]

MOdify it in the Focus property
```js
import React from 'react';
import { Text, View, StyleSheet } from 'react-native';
import {TextInput} from "react-native-paper";
import {RoundedButton} from "../../components/RoundedButton"

export const Focus = () => {
  return (
    <View style={styles.component}>
      <View style={styles.componentTitle}>
        <Text style={styles.titleText}>What would you like to focus on? </Text>
        <View style={styles.inputBox}>
          <TextInput />
          <RoundedButton title="+" size={50} />
        </View>
      </View>
    </View>
  );
}
```
![[Pasted image 20220718121256.png]]

To make this horizontally alligned with the text input, we modify the styling. We turn the container into a `flexDirection: "row"` then make the texinput grow into maximum by applying `flex: 1`
```js
const styles = StyleSheet.create({

  component: {
    flex: 1,
  },
  componentTitle: {
    flex: 0.5,
    padding: 16,
    justifyContent: "center"
  },
  titleText: {
    fontSize: 24,
    fontWeight: "bold",
    color: "white"
  },
  inputBox: {
    marginTop: 20,
    flexDirection: "row"
  }
});
```

```js
import React from 'react';
import { Text, View, StyleSheet } from 'react-native';
import {TextInput} from "react-native-paper";
import {RoundedButton} from "../../components/RoundedButton"

export const Focus = () => {
  return (
    <View style={styles.component}>
      <View style={styles.componentTitle}>
        <Text style={styles.titleText}>What would you like to focus on? </Text>
        <View style={styles.inputBox}>
          <TextInput style={{flex: 1}} />
          <RoundedButton title="+" size={50} />
        </View>
      </View>
    </View>
  );
}
```


```ad-Danger
collapse: open
On TouchableOpacity, we do not use `onClick` method to create an event, but `onPress` method

```

Next is how to make this inputs functional, click [[Functional Buttons]]
