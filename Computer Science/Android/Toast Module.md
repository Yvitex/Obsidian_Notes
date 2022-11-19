---
aliases: []
---
A [[JAVA]] or android module that will output an overlayed text like an important information below the screen. We will use the third way of [[Click Listener in Android]]. 
![[Pasted image 20221017050550.png]]

Set the see status button with an event listener by appending the code
```xml
android:onClick="toastShow"
```

Create a `toastShow` function and check if it is working
```java
public  void toastShow(View view){  
    Log.d("toastShow", "Working");
}
```

If it is working, then use the `Toast` module
```java
public  void toastShow(View view){  
    Toast.makeText();  
}
```

We need 3 arguments in this method. The first is the context, the context is the overall layout of the application and we need to provide it so the toast know where to put itself into. The second argument is the message, it could be a pure String or get the string from the [[String.xml]]. The third and last argument is the length or duration of the string, we could choose either short or long. Don't forget to call the chained method `.show()` to display it
```java
Toast.makeText(MainActivity.this, "hello world-chan", Toast.LENGTH_SHORT).show();
```

Or using the resources
```java
Toast.makeText(MainActivity.this, R.String.info, Toast.LENGTH_SHORT).show();
```

Where info is
```xml
<string name="info">Hello World-San</string>
```











# Metatags
###### Related: 
###### Tags: #java-module 
###### Source: 

---