---
aliases: []
---
A hidden textView or any kind of [[Android View Class]] that we set `visibility` to hidden in the [[Android Attributes]]. 

So we have this application
![[Pasted image 20221021111222.png]]

We want to enter the hobbies of user and reveal it to a certain textview just below the Button. The id of the components are the following:
- hobbyInput = text input where you enter the hobbies
- hiddenText = the hidden text where we will show their hobbies
- submitMyHobbies = the button with done as text

First, we initialize the variables in the very start of of class MainActivity
```java
private EditText submittedHobbies;  
private TextView userHobbies;  
private Button submitButton;
```

Then set the component to these variables after the [[setContentView Android]]
```java 
submittedHobbies = findViewById(R.id.hobbyInput);  
userHobbies = findViewById(R.id.hiddenText);  
submitButton = findViewById(R.id.submitMyHobbies);
```

Create a [[Click Listener in Android]]
```java
submitButton.setOnClickListener(new View.OnClickListener(){
	@Override
	public void onClick(View view){
		
	}
})
```

Set the text of userHobbies with the value f the submittedHobbies and turn it into a string, trim it also. 
```java
submitButton.setOnClickListener(new View.OnClickListener(){
	@Override
	public void onClick(View view){
		userHobbies.setText(submittedHobbies.getText().toString().trim());
	}
})
```

Set the visibility using `setVisibility()` to visible using the View
```java
submitButton.setOnClickListener(new View.OnClickListener(){
	@Override
	public void onClick(View view){
		userHobbies.setText(submittedHobbies.getText().toString().trim());
		userHobbies.setVisibility(View.VISIBLE);
	}
})
```

![[Pasted image 20221021140244.png]]

It should work. We could [[Remove the Keyboard]] at clicking done. 











# Metatags
###### Related: 
###### Tags: 
###### Source: 

---