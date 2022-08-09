# Timer
Import the [[React Native Boiler Plate]]. Start by printing out a simple text. 
```js
import React from "react";
import {StyleSheet, View, Text} from "react-native";

export const Countdown = () => {
	return <View>
		<Text>Countdown Goes here<Text>
	</View>
}
```

![[Pasted image 20220719091546.png]]

```js

export const Countdown = () => {
	return <View>
		<Text style={styles.text}>Countdown Goes here<Text>
	</View>
}

const styles = StyleSheet.create({
  container: {
    flex: 1
  },
  text: {
    color: colors.whiteFont,
    fontSize: fontSizes.xxl,
    textAlign: "center",
    backgroundColor: "rgba(94, 132, 226, 0.3)",
    padding: sizes.lg
  }
})
```
![[Pasted image 20220719091635.png]]

We need to convert it into time, first is that we need this time to be user chosen so we create a [[React Properties]] of minutes and pause state
```js
export const Countdown = ({
	minutes = 20, 
	isPaused,
}) => {
	return <View>
		<Text style={styles.text}>Countdown Goes here<Text>
	</View>
}
```

[[Javascript]] works with milliseconds. Make a function that convert minutes to milliseconds
```js

const minutesToMillis = (minutes) => minutes * 60 * 1000;

export const Countdown = ({
	minutes = 20, 
	isPaused,
}) => {
	return <View>
		<Text style={styles.text}>Countdown Goes here<Text>
	</View>
}
```

Create a [[Hooks]] that will initially hold this convertion.
```js
const minutesToMillis = (minutes) => minutes * 60 * 1000;

export const Countdown = ({
	minutes = 20, 
	isPaused,
}) => {

	const [millis, setMillis] = useState(minutesToMillis);
	
	return <View>
		<Text style={styles.text}>{millis}<Text>
	</View>
}
```
![[Pasted image 20220719092251.png]]

We need to convert this milliseconds in a time like minutes: second format. Create an [[Expression vs Statement|expression]] that will convert them into that format.
```js
const minutesToMillis = (minutes) => minutes * 60 * 1000;

export const Countdown = ({
	minutes = 20, 
	isPaused,
}) => {

	const [millis, setMillis] = useState(minutesToMillis);
	let millisToMinutes = Math.floor(millis / 1000 / 60);
	let millisToSeconds = Math.floor(millis / 1000) % 60;
	
	return <View>
		<Text style={styles.text}>{millisToMinutes} : {millisToSeconds}<Text>
	</View>
}
```

![[Pasted image 20220719092753.png]]

We need to create a function that when the seconds is less than 10, it will add a zero before the actual seconds
```js
const minutesToMillis = (minutes) => minutes * 60 * 1000;
const appendZero = (seconds) => seconds < 10 ? `0${seconds}` : seconds;

export const Countdown = ({
	minutes = 20, 
	isPaused,
}) => {

	const [millis, setMillis] = useState(minutesToMillis);
	let millisToMinutes = Math.floor(millis / 1000 / 60);
	let millisToSeconds = Math.floor(millis / 1000) % 60;
	
	return <View>
		<Text style={styles.text}>{millisToMinutes} : {appendZero(millisToSeconds)}<Text>
	</View>
}
```
![[Pasted image 20220719093119.png]]


Now, how to make the [[Countdown counting down]]
