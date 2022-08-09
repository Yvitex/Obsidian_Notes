# Text Input
We could use libraries to create this stuff. In our case, we will use, [[React-Native-Paper]]. In [[Expo]], we could include this by typing the name directly to the dependencues along with the version number
![[Pasted image 20220718095859.png]]

Import it to the component, remember that styling must be done by components and nt on the renderer, we specifically input the `{TextInput}`
```js
import {TextInput} from "react-native-paper";
```

We will took the code we created from the last lesson about [[React Native Component]]
```js
import React from 'react';
import { Text, View, StyleSheet } from 'react-native';
import {TextInput} from "react-native-paper";

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

We could add the imported component
```js
import React from 'react';
import { Text, View, StyleSheet } from 'react-native';
import {TextInput} from "react-native-paper";

export const Focus = () => {
  return (
    <View style={styles.component}>
      <Text> Rendering none </Text>
      <TextInput />
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

We usually add styling by creating View element then applying the styles to those elements. But it is optional, we could apply some components directly but using View element, we could make the use of flex property more effectively
```js
export const Focus = () => {
  return (
    <View style={styles.component}>
      <View style={styles.componentTitle}>
        <Text style={styles.titleText}>What would you like to focus on? </Text>
        <View style={styles.inputBox}>
          <TextInput />
        </View>
      </View>
    </View>
  );
}

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
    marginTop: 20
  }
});
```

![[Pasted image 20220718101531.png]]

