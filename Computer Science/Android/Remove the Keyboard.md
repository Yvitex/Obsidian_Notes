---
aliases: []
---
We could remove the keyboard in the screen after an event using this code in [[Android Studio]].

We will control the code using a variable of type `InputMethodManager`
```java
InputMethodManager inputManager = null;
```

We will assign the value of input method service using the `getSystemService` method
```java
InputMethodManager inputManager = getSystemService(Context.INPUT_METHOD_SERVICE);
```

THis won't work, convert the assigned valeu to InputMethodManager
```java
InputMethodManager inputManager = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
```

We could then use the variable and call the hide method which is `hideSoftInputFromWindow()`
```java
InputMethodManager inputManager = getSystemService(Context.INPUT_METHOD_SERVICE);
inputManager.hideSoftInputFromWindow()
```

This method will accept 2 arguments, one is the token which we could get inside the view variable of an eventListener. The second argument is the number of flag which we could set as 0

```java
submitButton.setOnClickListener(new View.OnClickListener(){
	@Override
	public void onClick(View view){
		InputMethodManager inputManager = getSystemService(Context.INPUT_METHOD_SERVICE);
		inputManager.hideSoftInputFromWindow(view.getWindowToken(), 0);
	}
})
```

That's it. 










# Metatags
###### Related: 
###### Tags: 
###### Source: 

---