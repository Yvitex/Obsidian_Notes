# Progress Bar
[[React-Native-Paper]] also has this component called `ProgressBar`

To import it to our code, we simply do this
```js
import { ProgressBar } from "react-native-paper"

<ProgressBar />
```

It will the `progress` properties. We could also change the color by setting the `color` properties
```js
<ProgressBar 
	style={{height: 10}}
	color="#5E84E2"
	progress={}
/>
```

We need to pass some value to that property from 0 to 1 and because it is a changing state, we need to include some [[Hooks]]
```js
export const Timer = ({ focusSubject }) => {
  const [isStarted, setIsStarted] = useState(false);
  const [progress, setProgress] = useState(1);
  
  return (
    <View style={styles.container}>
      <View style={styles.timerContainer}>
        <Countdown isPaused={!isStarted} />
      </View>
      <View style={styles.textContainer}>
        <Text style={styles.textStyles}>Focusing on:</Text>
        <Text style={[styles.textStyles, styles.boldSubstance]}>
          {focusSubject}
        </Text>
      </View>
      <ProgressBar 
          style={{height: 10}}
          color = "#5E84E2"
          progress={progress}
       />

      <View style={styles.buttonContainer}>
      <RoundedButton 
        title = {isStarted ?  "Pause" : "Play"} 
        onPress = {() => {
        setIsStarted(!isStarted)
        }}
       />  
       
      </ View>
    </View>

  );

};
```

We set the initial state first to 1, because it is a countdown. We set it to the `progress` property. We need to create a function that will get the value from the other side of the component, in an external component
```js
function updateProgressStatus(progressStatus){
	
}
```

This will update the [[hooks]] depending on what the callback would fetch
```js
function updateProgressStatus(progressStatus){
	setProgress(progressStatus);
}
```

And we will set this function to fetch from the `<CountDown />` component
```js
<CountDown isPaused={!isStarted} onProgress={updateProgressStatus} />
```

We use the art of creating [[React Properties]] in the name of `onProgress`. In the external code, inside the `CountDown` function we look for a place where we could get the seconds left and the main seconds, we divide them to get the decimal value or the percentage that will be passed to the progress
```js
const startCountdown = () => {
    setMillis((time) => {
      if (time === 0) {
        return time;
      } else {
        let timeLeft = time - 1000;
        onProgress(timeLeft / minutesToMillis(minutes)) // pass the percentage using the onProgress property
        return timeLeft;
      }
    });
  };
```

![[chrome-capture-2022-6-19 (5).gif]]



