---
aliases: [java]
---
# Java Basics
Java is a [[Compiled Language]], while others such as [[Python Programming|python]] and [[Javascript]] are [[Interpreted language]]. That is why this has a lot more features than the others, but because it is compacted with features means it is a lot more complicated causing migrain. Please, send help.


## Make Buttons Functionable
First of, I deleted the content in the textView widget from [[User Interface Basics]] lesson
![[Pasted image 20220616052336.png]]

In the java file. I created 2 private variables that will get the 2 UI components(button , textView). The syntax goes like
```
private Button myButton;
private TextView myText;
```

These are set as global variables. At first, it will cause an error but you just need to import the necessary files such as 
```
import android.widget.Button;  
import android.widget.TextView;
```

Next, inside the `@Override` syntax. We set the right methods to make button functionable
```
@Override  
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    setContentView(R.layout.activity_main);   
}
```

Take note that, `setContentView(R.layout.activity_main);` enanle us to use the xml file from the [[User Interface Basics]] lesson named **activity_main.xml**. ![[Pasted image 20220616054151.png]]

Next is to store the widget inside the private variables. We could select the *id* of the widget by using `findViewByUserId(R.id)` method

```
@Override  
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    setContentView(R.layout.activity_main);   
	myButton = findViewById(R.id.button); // button is the id of the button
	myText = findViewById(R.id.textView); // button is the id of the button


}
```

Now, we could basically  set the text into anything by saying

```
@Override  
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    setContentView(R.layout.activity_main);   
	myButton = findViewById(R.id.button); // button is the id of the button
	myText = findViewById(R.id.textView); // button is the id of the button

	myText.setText("hello domo");
}
```

![[Pasted image 20220616054837.png]]


To make the text appears, only when button is pressed, we could use the `setOnClickListener()` method to do so. Inside the argument field, we create a callback function of the sort that will make the text render

```
@Override  
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    setContentView(R.layout.activity_main);   
	myButton = findViewById(R.id.button); // button is the id of the button
	myText = findViewById(R.id.textView); // button is the id of the button

	myButton.setOnClickListener(new View.OnClickListener(){
		@Override
		public void onClick(View view){
			myText.setText("Hello Domo");
		}
	});

}
```

Still, this is not very cool program and still static. Moving on, how can we create a dynamic greeting that will mention the user. 

![[Pasted image 20220616150502.png]]

We will set a plain text, which is actually an EditText. Here, we could edit what is inside the textbox, we could also set the *hint* attribute that in this picture, displays the  **Enter Name** string in low opacity, I also set the id of the widget to my own preference. 
![[Pasted image 20220616150755.png]]

Now we repeat the process of setting the widget to a variable. Inside the JAVA file. we set the variable as private
```
private EditText nameText;
```

The class should be an `EditText` then we will set the widget to the variable. 
```
nameText = findViewById(R.id.editName);
```

Of course, this do happen inside the `onCreate()`  method.  Now, inside the `setOnClickListenter` method, we create a `String` variable that will hold the extracted text from the `nameText` variable. 
```
myButton.setOnClickListener(new View.OnClickListener(){  
    @Override  
    public void onClick(View view){  
        String name = nameText.getText().toString();  
});
```

What will happen if the user does not enter any input string? Then we could do an if-else statement to control it such as

```
myButton.setOnClickListener(new View.OnClickListener(){  
    @Override  
    public void onClick(View view){  
        String name = nameText.getText().toString();
        if(name.isEmpty()){
	        myText.setText("Hello, Anonymous")
        }  
});
```

`isEmpty()` detects if a variable is empty. Matching the if statement, we have an else statement where when the user types in a value, then we will allocate that value to the part where we will set the text greeting.

```
myButton.setOnClickListener(new View.OnClickListener(){  
    @Override  
    public void onClick(View view){  
        String name = nameText.getText().toString();
        if(name.isEmpty()){
	        myText.setText("Hello, Anonymous");
        }  
        else{
	        myText.setText("Hello, " + name);
        }
});
```

It's already familiar as it is the same with [[Python Programming]] and [[Javascript]] . So when we enter a name, the device will look like this
![[Pasted image 20220616152635.png]]
If we leave it blank, it will look like this. 
![[Pasted image 20220616152703.png]]


Well, all well and good until you realize that... this is a very specifc java syntax heavily used at [[Android Programming (Core)]] and not Java by itself. However, we could create a module with pure java code by creating a new library. Read, how to [[lsolating  Java From Android Studio]]


