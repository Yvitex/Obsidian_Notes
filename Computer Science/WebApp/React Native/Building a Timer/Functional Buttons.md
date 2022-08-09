# Functional Buttons
`TouchableOpacity` use the `onPress` method rather than `onClick` and `TextInput` from [[React-Native-Paper]] 

From example from [[Creating a Button]]
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
```

We apply touchableopacity's  onPress method that will be passed as a [[React Properties]]

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
	 <TouchableOpacity onPress={props.onPress} style={[styles, styles(size).radius]}> // Applied onPress method
     <Text style={[textStyle, styles(size).innerText]}>{props.title}</Text>
     </TouchableOpacity>
  ); 
}
```

The on press method will be passed from the Focus file in `RoundedButton`
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
          <RoundedButton onPress={() => null} title="+" size={50} />
        </View>
      </View>
    </View>
  );
}
```

We know that we are passing a function, it will just immediately execute when it have parameters, so we may like to use the arrow function
In the main app code, we may want to print the focus subject code
```js
export default function App() {
  const [focusSubject, setFocusSubject] = useState(null);
  return (
    <View style={styles.component}>
      {focusSubject != null ? <Text>Have state</Text> : <Focus />}
      <Text>{focusSubject}</Text>
    </View>
  );
}
```

We also want to set the [[Hooks]] so that when there is no `focusSubject` we are prompted to the input and that input could modify the [[Hooks]] of the `focusSubject`
```js
export default function App() {
  const [focusSubject, setFocusSubject] = useState(null);
  return (
    <View style={styles.component}>
      {focusSubject != null ? <Text>Have state</Text> : <Focus addSubject={setFocusSubject}/>}
      <Text>{focusSubject}</Text>
    </View>
  );
}
```

We pass the function `setFocusSubject` so that we could pass an argument that will change the initial state.  We pass this [[React Properties]] to the child file.
```js
export const Focus = ({addSubject}) => {
  return (
    <View style={styles.component}>
      <View style={styles.componentTitle}>
        <Text style={styles.titleText}>What would you like to focus on? </Text>
        <View style={styles.inputBox}>
          <TextInput style={{flex: 1}} />
          <RoundedButton onPress={() => null} title="+" size={50} />
        </View>
      </View>
    </View>
  );
}
```

We pass it as a [[Destructuring]] object rather than using `props` as we want it to be specific. 

`TextInput` from [[React-Native-Paper]] have this property called `onSubmitEdit`. `onSubmitEdit` will have a callback called `nativeEvent` that contains the text inside `nativeEvent.text`
```js
export const Focus = ({addSubject}) => {
  return (
    <View style={styles.component}>
      <View style={styles.componentTitle}>
        <Text style={styles.titleText}>What would you like to focus on? </Text>
        <View style={styles.inputBox}>
          <TextInput 
	          onSubmitEditing={(nativeEvent) => {addSubject(nativeEvent.text)}} 
	          style={{flex: 1}} />
          <RoundedButton onPress={() => null} title="+" size={50} />
        </View>
      </View>
    </View>
  );
}
```
![[chrome-capture-2022-6-19.gif]]

The button is not working, but when we press return in the keyboard, it will execute the `onSubmitEditing`. To make things right and only submit the code, we could create another [[Hooks]] that will handle it and pass the initial to the `onPress` property

```js
export const Focus = ({addSubject}) => {

	const [tmpState, setTmpState] = useState(null);

   return (
    <View style={styles.component}>
      <View style={styles.componentTitle}>
        <Text style={styles.titleText}>What would you like to focus on? </Text>
        <View style={styles.inputBox}>
          <TextInput 
	          onSubmitEditing={(nativeEvent) => {setTmpState(nativeEvent.text)}} 
	          style={{flex: 1}} />
          <RoundedButton 
	          onPress={() => addSubject(tmpState)}
	          title="+" 
	          size={50} />
        </View>
      </View>
    </View>
  );
}
```
![[chrome-capture-2022-6-19 (1).gif]]



The next step to take is to design the reroute page when the the [[Hooks]] in the app jsx file changes state, let's call it [[Rerouting and Styling]]




