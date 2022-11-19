---
aliases: []
---
![[Pasted image 20221025110845.png]]


```java
@Override  
protected void onCreate(Bundle savedInstanceState) {  
    super.onCreate(savedInstanceState);  
    setContentView(R.layout.activity_main);
}
```
 
 `onCreate()` method is created at execution then to the `onStart()`. `onResume()` wil then finally come and make the application running but on the event that there is an interruption such as phone call, `onPause()` will execute which will then desides to `onRestart()` or do again the `onCreate()` from the start or `onDestroy()` which we completely shutdown the application. 

The lifecycle methods will help us understand when to do something, for example, saving the user data at `onDestroy()` method to retain the information. 

We could actually implement this by code.
```java
@Override  
protected void onStart() {  
    super.onStart();  
}  
  
@Override  
protected void onPostResume() {  
    super.onPostResume();  
}  
  
@Override  
protected void onPause() {  
    super.onPause();  
}  
  
@Override  
protected void onStop() {  
    super.onStop();  
}  
  
@Override  
protected void onDestroy() {  
    super.onDestroy();  
}  
  
@Override  
protected void onRestart() {  
    super.onRestart();  
}
```

To test things out, we will output the state of the lifecycle in the debugger
```java
@Override  
protected void onStart() {  
    super.onStart();  
    Log.d("Life Cycle", "onStart()");  
}  
  
@Override  
protected void onPostResume() {  
    super.onPostResume();  
    Log.d("Life Cycle", "onResume()");  
}  
  
@Override  
protected void onPause() {  
    super.onPause();  
    Log.d("Life Cycle", "onPause()");  
}  
  
@Override  
protected void onStop() {  
    super.onStop();  
    Log.d("Life Cycle", "onStop()");  
}  
  
@Override  
protected void onDestroy() {  
    super.onDestroy();  
    Log.d("Life Cycle", "onDestroy()");  
}  
  
@Override  
protected void onRestart() {  
    super.onRestart();  
    Log.d("Life Cycle", "onRestart()");  
}
```

When we open the app, these are the method being executed
![[Pasted image 20221025114311.png]]

When we press exit these are the methods
![[Pasted image 20221025114341.png]]

If we just press the home button without exiting the app as well as going to another app
![[Pasted image 20221025114421.png]]

When we re enter to it once again
![[Pasted image 20221025114503.png]]


# Metatags
###### Related: 
###### Tags: 
###### Source: 

---