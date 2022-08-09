# CountDown
From our lesson in [[Creating a Countdown Timer]], we will now set the timer running. But first, we add some styling for the application. We wrap the element timer to a View element
```js
export const Timer = ({ focusSubject }) => {
  return (
    <View style={styles.container}>
      <View style={styles.timerContainer}>
        <Countdown />
      </View>
      <View style={{ paddingTop: sizes.xxl }}>
        <Text style={styles.textStyles}>Focusing on:</Text>
        <Text style={[styles.textStyles, styles.boldSubstance]}>
          {focusSubject}
        </Text>
      </View>
    </View>
  );
};
```

To that styling, we add a textStyles properties object
```js
const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  textStyles: {
    color: colors.whiteFont,
    textAlign: 'center',
  },
  boldSubstance: {
    fontWeight: 'bold',
  },
  timerContainer: {
    flex: 0.5,
    alignItems: "center",
    justifyContent: "center"
  }
});
```

Basicaly, we set it on flex and align in row and column as center.
Moving on to the Timer component. We create another function that will store the set [[hooks]] method that will change the time in seconds
```js
export const Countdown = ({
	minutes = 20, 
	isPaused,
}) => {
	const [millis, setMillis] = useState(minutesToMillis);
	let millisToMinutes = Math.floor(millis / 1000 / 60);
	let millisToSeconds = Math.floor(millis / 1000) % 60;

	const startCountDown = () => {
		setMillis(); // we'll set the seconds here
	}
	
	return <View>
		<Text style={styles.text}>{millisToMinutes} : {appendZero(millisToSeconds)}<Text>
	</View>
}
```

Using this, we wll fetch previous state of the [[Hooks]] then subtract it by 1000. The result will is what returned to the `setMillis` method
```js
export const Countdown = ({
	minutes = 20, 
	isPaused,
}) => {
	const [millis, setMillis] = useState(minutesToMillis);
	let millisToMinutes = Math.floor(millis / 1000 / 60);
	let millisToSeconds = Math.floor(millis / 1000) % 60;

	const startCountDown = () => {
		setMillis((time) => {
			return time - 1000;
		}); // fetch the previous state then substract
	}
	
	return <View>
		<Text style={styles.text}>{millisToMinutes} : {appendZero(millisToSeconds)}<Text>
	</View>
}
```

But it will go pass through negative like this. We need to stop it when it comes down to zero so we use an if else statement.
```js
export const Countdown = ({
	minutes = 20, 
	isPaused,
}) => {
	const [millis, setMillis] = useState(minutesToMillis);
	let millisToMinutes = Math.floor(millis / 1000 / 60);
	let millisToSeconds = Math.floor(millis / 1000) % 60;

	const startCountDown = () => {
		setMillis((time) => {
	      if(time === 0){
	        return time;
	      }
	      else{
	        return time - 1000;
	      }
	    })
		}
	
	return <View>
		<Text style={styles.text}>{millisToMinutes} : {appendZero(millisToSeconds)}<Text>
	</View>
}
```

We will then utilize the `setInterval` method of [[Javascript]] to execute this function repeatedly until it returns 0. But the plot twist is that it does not work correctly inside react. we need a way to make this right and that is by using the [[useEffect]] method

First is we import this `useEffect` method and `useRef`. [[useRef]] Will store the current value.
```js
import React, {useState, useEffect, useRef} from "react";
```

Set the `useRef` thing to a variable and this will accept an argument of `null`
```js
export const Countdown = ({
	minutes = 20, 
	isPaused,
}) => {
	const [millis, setMillis] = useState(minutesToMillis);
	let millisToMinutes = Math.floor(millis / 1000 / 60);
	let millisToSeconds = Math.floor(millis / 1000) % 60;
	const interval = useRef(null); // set useRef to null

	const startCountDown = () => {
		setMillis((time) => {
	      if(time === 0){
	        return time;
	      }
	      else{
	        return time - 1000;
	      }
	    })
		}
	
	return <View>
		<Text style={styles.text}>{millisToMinutes} : {appendZero(millisToSeconds)}<Text>
	</View>
}
```

Create a useeffect method and inside the function argument, we will fetch the `current` variable from the `useRef` referrence and set it to the return value of startCountdown in an interval
```js
useEffect(() => {
	interval.current =  setInterval(startCountdown, 1000); // every 1 second execution
})
```
![[chrome-capture-2022-6-19 (2).gif]]

We use the `useEffect` method to stabilize this problem we have. In return, we could pass a function that will clear the interval to fix our problem
```js
useEffect(() => {
	interval.current =  setInterval(startCountdown, 1000); // every 1 second execution
	return () => {clearInterval(interval.current)}
})
```

What we will clear is the `useRef` 's `current` variable
![[chrome-capture-2022-6-19 (3).gif]]

Next is to set the button that will [[Control Countdown]]
