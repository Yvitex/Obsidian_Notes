# Rerouting
As we could see from the [[Functional Buttons]] section, 
![[chrome-capture-2022-6-19 (1).gif]]

The design of the second page is not very good. We create a new component in a new file called `Timer.js`
This timer js will return this.
```js
export const Timer = () => {
  return (
    <View style={styles.container}>
      <View >
        <Text>Focusing on:</Text>
        <Text>focusSubject</Text>
      </View>
    </View>
  );
};
```

This will have a [[React Properties]] that will be passed as second text.
```js
export const Timer = ({focusSubject}) => {
  return (
    <View style={styles.container}>
      <View >
        <Text>Focusing on:</Text>
        <Text>{focusSubject}</Text>
      </View>
    </View>
  );
};
```

In the app file
```js
export default function App() {
  const [focusSubject, setFocusSubject] = useState("gardening");
  return (
    <View style={styles.component}>
      {focusSubject != null ? <Timer focusSubject={focusSubject} /> : <Focus addSubject={setFocusSubject}/>}
    </View>
  );
}
```

We import the `Timer` component and use the name `focusSubject` to pass the `focusSubject` variable.
![[Pasted image 20220719081253.png]]

Not good. We need to style it, the parent element must have the `flex: 1` grow property, we need to allign all the text and make it color white
```js
const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  textStyles: {
    color: colors.whiteFont,
    textAlign: "center",
  },
  boldSubstance: {
    fontWeight: "bold",
  }
});
```

We could apply it to each element
```js
export const Timer = ({ focusSubject }) => {
  return (
    <View style={styles.container}>
      <View style={{paddingTop: sizes.xxxl}}>
        <Text style={styles.textStyles}>Focusing on:</Text>
        <Text style={[styles.textStyles, styles.boldSubstance]}>{focusSubject}</Text>
      </View>
    </View>
  );
};
```

Refer to the [[Styling With Consistency]] 
```ad-Notice
collapse: open
Notice that the parent element have its own life and only act as a container with flex value, nothing else. It is always better to create a new View element if possible. 

```

![[Pasted image 20220719081726.png]]

Now we could start [[Creating a Countdown Timer]]