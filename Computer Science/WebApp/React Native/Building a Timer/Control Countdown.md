# Controls
From the the code at [[Countdown counting down]]
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
		
	useEffect(() => {
	interval.current =  setInterval(startCountdown, 1000); // every 1 second execution
	return () => {clearInterval(interval.current)}
})

	return <View>
		<Text style={styles.text}>{millisToMinutes} : {appendZero(millisToSeconds)}<Text>
	</View>
}
```

We will use the `isPaused` [[React Properties]] to check if we want it paused and if yes, we will create an if statement that will exit the function immediately inside the [[useEffect]] method as it is the core of the interval
```js
	useEffect(() => {
	if(isPaused){
		return;  // Return nothing
	}
	interval.current =  setInterval(startCountdown, 1000); // every 1 second execution
	return () => {clearInterval(interval.current)}
})
```

In the external component, we will make use of the [[React Properties]] called `isPaused` in which we will pass if it is true or false.
```js
export const Timer = ({ focusSubject }) => {
  return (
    <View style={styles.container}>
      <View style={styles.timerContainer}>
        <Countdown isPaused={true} /> // set isPaused property to true
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

We may want to do this but we want a dynamic state that will determine if we want the program to run and can revert into its recirprocal. So in this case, we may want to use [[Hooks]]
```js
export const Timer = ({ focusSubject }) => {

	const [isStarted, setIsStarted] = useState(false); // default in false

	  return (
	    <View style={styles.container}>
	      <View style={styles.timerContainer}>
	        <Countdown isPaused={!isStarted} /> // this will pause the timer
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

We want a way to change the state of the `isStarted` initial variable so therefore we create a button to make use of it. We will use what we created in [[Creating a Button]] section.
```js
export const Timer = ({ focusSubject }) => {

	const [isStarted, setIsStarted] = useState(false); // default in false

	  return (
	    <View style={styles.container}>
	      <View style={styles.timerContainer}>
	        <Countdown isPaused={!isStarted} /> // this will pause the timer
	      </View>
	      <View style={{ paddingTop: sizes.xxl }}>
	        <Text style={styles.textStyles}>Focusing on:</Text>
	        <Text style={[styles.textStyles, styles.boldSubstance]}>
	          {focusSubject}
	        </Text>
	      </View>
	      <RoundedButton title="play" /> // create button that with play title
	    </View>
	  );
	};
```

![[Pasted image 20220719122327.png]]

On Click, we will execute a function that will change the state of our current [[Hooks]] called `isStarted`, but we also want this button to revert back into the previous state when click again, so we do this
```js
 <RoundedButton 
	 title={isStared ? "Pause" : "Play"} 
	 onPress={() => {setIsStarted(!isStarted)}} 
/>
```

![[chrome-capture-2022-6-19 (4).gif]]


The only thing left to do is some styling
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
    alignItems: 'center',
    justifyContent: 'center',
  },
  buttonContainer: {
    alignItems: "center",
    justifyContent: "center",
    flex: 0.5
  }
});
```

```js
<View style={styles.buttonContainer}>
      <RoundedButton 
        title = {isStarted ?  "Pause" : "Play"} 
        onPress = {() => {
          setIsStarted(!isStarted)
        }}
        />
      </ View>
```

![[Pasted image 20220719123235.png]]


We centered it by a couple of [[Flex-grow]] and [[Css Alignments]].

What's next is [[Creating the Progress Bar]]

