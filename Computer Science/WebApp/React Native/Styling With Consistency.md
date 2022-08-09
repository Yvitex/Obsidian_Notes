# Styling
We need to be consistent with our styling and in order to do that, we may want to create a storage file in which we will grab the only source of truth.

![[Pasted image 20220719050830.png]]

Create a new folder called utils, create new files that will store the constant variabels.
Inside the sizes file, create a variable constant that is to be exported
```js
export const fontSizes = {
  sm: 8,
  md: 16,
  lg: 24, 
  xl: 32,
  xxl: 40,
  xxxxl: 80,
}
```

Also create the sizes variable.
```js
export const fontSizes = {
  sm: 8,
  md: 16,
  lg: 24, 
  xl: 32,
  xxl: 40,
  xxxxl: 80,
}

export const sizes = {
  sm: 8,
  md: 16,
  lg: 24, 
  xl: 32,
  xxl: 40,
  xxxxl: 80,
}
```

[[Importing in Javascript|import]] it to the other file and change hardcoded code to this things. From our code in the last lesson about [[Creating a Button]], we could change them from hardcoded styling to something
```js
const styles = StyleSheet.create({

  component: {
    flex: 1,
  },
  componentTitle: {
    flex: 0.5,
    padding: sizes.md,
    justifyContent: "center"
  },
  titleText: {
    fontSize: sizes.lg,
    fontWeight: "bold",
    color: "white"
  },
  inputBox: {
    marginTop: sizes.md,
    flexDirection: "row"
  }
});
```

