---
aliases: []
---
![[Pasted image 20221025144701.png]]

To create multiple activity, we first need to create that new activity in which we could add by going to files > new file > Activity > Empty Activity

After creating this, it will have its own Activty [[JAVA]] file and also [[Android Studio|xml]]. So I created 2 activities, 
![[Pasted image 20221025151531.png]]

The first one is the main which have a button and a plain text. The second one is this:
![[Pasted image 20221025151605.png]]

Which contains an empty textview. If we want to go to the second activity from the first, we are going to use an Intent class. 
Using [[Data Binding - Binding Views]], i create a [[Click Listener in Android]] in which if I click the button, I go to the second activity. Set the Intent class and speciffy from where do we start and then the destination
The code is this:
```java
binding.submitButton.setOnClickListener(view -> {  
    Intent intent = new Intent(MainActivity.this, ShowGuess.class);  
});
```

Now, activate the intent using `startActivity()`.
```java
binding.submitButton.setOnClickListener(view -> {  
    Intent intent = new Intent(MainActivity.this, ShowGuess.class);  
    startActivity(intent);  
});
```

THis should work. We could pass the information from the plain text to the second activity using `putExtra` method of the intent. This should be a key value pair, we will pass the data from the binder [[Android Studio|xml]] and since we want this as string, we convert the value to string
```java
binding.submitButton.setOnClickListener(view -> {  
    Intent intent = new Intent(MainActivity.this, ShowGuess.class);  
    intent.putExtra("guess", binding.textGuess.getText().toString().trim());  
    startActivity(intent);  
});
```

Our key is "guess" and the data we have is from the plain text, we get this, convert to string and trimmed.

In the logic of second activity, we could retrieve this using `getIntent()`. We first check if the extra is null then we store it to a variable string, or not. And then pass it as a text of the text view. 
```java
showGuess = findViewById(R.id.showTheGuess);

if(getIntent().getStringExtra("guess") != null){
	String userGuess = getIntent().getStringExtra("guess");
	showGuess.setText(userGuess);
}
```

![[Pasted image 20221025160156.png]]

![[Pasted image 20221025160205.png]]


Also we could have multiple extras like this
```java
binding.submitButton.setOnClickListener(view -> {  
    Intent intent = new Intent(MainActivity.this, ShowGuess.class);  
    intent.putExtra("guess", binding.textGuess.getText().toString().trim());  
    intent.putExtra("name", "Mitty");  
    intent.putExtra("age", 12);  
    startActivity(intent);  
});
```

The best way to store this is through a Bundle in th second activity.
```java
Bundle extras = getIntent().getExtras();
```

We could then get the datas by using `getInt()` or `getString()` depending on the [[Java Variables|data type]] with argument of the key name
```java
if(extras.getString("guess") != null){  
    Log.d("Extras", "Name: " + extras.getString("name"));  
    Log.d("Extras", "Age: " + extras.getInt("age"));  
    String extraIntent = getIntent().getStringExtra("guess");  
    showGuess.setText(extraIntent);  
}
```

# Metatags
###### Related: [[Android Studio]]
###### Tags: 
###### Source: 

---