# Click Listener
We already know the [[Java Basics]] for android
There are 3 ways we could approach this. Using the user interface in [[String.xml]], we renamed each button with speciified id.
![[Pasted image 20220711150841.png]]

```java
package com.example.makeitrain;  
  
import androidx.appcompat.app.AppCompatActivity;  
  
import android.os.Bundle;  
import android.util.Log;  
import android.view.View;  
import android.widget.Button;  
import android.widget.TextView;  
  
public class MainActivity extends AppCompatActivity {  
  
    private TextView moneyValue;  
    private Button miningButton;  
    private Button seeStatus;  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        setContentView(R.layout.activity_main);

		moneyValue = findViewById(R.id.moneyValue);  
		miningButton = findViewById(R.id.miningButton);  
		seeStatus = findViewById(R.id.seeStatusButton);
    }
```

## First way
The first way is the long method where we need to pass the View Object as a parameter and overriding the onClick method.
```java

miningButton.setOnClickListener(new View.onClickListener(){
	@Override
	public void onClick(View view){
		Log.d("Debug Test", "onClick: Confirmed");
	}
})
```

We use the Log.d method to see if it is working or not. THis have 2 parameter, the tag and the actual console printout. The tag will help us find the printout.

## Second Way
Shortest way to create a onclick listener by using an arrow function.
```java
miningButton.setOnClickListener(view -> Log.d("Debug Test", "onClick: Confirmed"));
```

## Third way
Using onClick method in xml
```xml
android:onClick="confirmClick"
```

In the MainActivity method, we add this to the main override
```java
public void confirmClick(View view){
	Log.d("Debug Test", "onClick: Confirmed");
}
```







