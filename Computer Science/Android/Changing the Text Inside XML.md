---
aliases: []
---
Using our make in rain app, it doesn't matter if you didn't know it but in this app, we are meant to increase the value at the screen by 1000 per click of a button.![[Pasted image 20221017050550.png]]

The first change we need to do is the display [[Android Studio|xml]]. Change the text from 2000 to 0 in the [[String.xml]]. 
```xml
<string name="moneyValue">$0.00</string>
```

The next tweak is modifying our code in the [[Click Listener in Android]] section. We will add another private variable called `valueCounter` that will start with 0
```java
private TextView moneyValue;  
private Button miningButton;  
private Button seeStatus;  
private int moneyCounter = 0;
```

Next when we click, we are supposed to increment this value by a thousand.
```java
@Override  
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    setContentView(R.layout.activity_main);  
  
    moneyValue = findViewById(R.id.moneyValue);  
    miningButton = findViewById(R.id.miningButton);  
    seeStatus = findViewById(R.id.seeStatusButton);  
    miningButton.setOnClickListener(new View.OnClickListener() {  
        @Override  
        public void onClick(View view) {  
		    // Here's the tweak
            moneyCounter += 1000;  
        }  
          
    });  
    }
```

Now, what we want to do is to repalce the text from the [[Android Studio|xml]] with the `moneyCounter` value. The variable to be modified is in the `moneyValue` variable
```java
@Override  
public void onClick(View view) {  
	moneyCounter += 1000;  
	moneyValue.setText(moneyCounter);
}  
```

Of course, this won't work. Not yet. We need to convert the integer into string so we use the String class that convert it so
```js
@Override  
public void onClick(View view) {  
	moneyCounter += 1000;  
	moneyValue.setText(String.valueOf(moneyCounter));
}
```

At this moment, it will work as we wanted, though there will be no dollar sign. What we could do is to convert this number into some currency using the [[NumberFormat]] class that comes with [[JAVA]]

Instantiate it into a variable and select the method that is a currency instance or, `getCurrencyInstance`
```java
@Override  
public void onClick(View view) {  
	NumberFormat numberFormat = NumberFormat.getCurrencyInstance();
	moneyCounter += 1000;  
	moneyValue.setText(String.valueOf(numberFormat.format(moneyCounter)));
}
```

Now clicking the button
![[Pasted image 20221017052628.png]]

We will get
![[Pasted image 20221017052648.png]]

